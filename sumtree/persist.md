

The sum+_ree itself is not persisted as a standalone on-disk format in the crate. In Zed, it’s mostly a persistent in-memory data structure: values are cloned through Arc, and snapshots keep old versions alive cheaply.

So the “persistence” code is really the code that stores a SumTree inside snapshot/state objects and reuses it across edits. The clearest places are:

* crates/text/src/text.rs  
  * BufferSnapshot / fragment building uses SumTree\<Fragment\>  
  * FragmentBuilder::to\_sum\_tree(...) builds a persistent tree for text fragments  
  * UndoMap and OperationQueue also keep tree-backed state across edits  
  
* crates/language/src/syntax\_map.rs  
  * SyntaxSnapshot stores layers: SumTree\<SyntaxLayerEntry\>  
  * its Drop implementation swaps in a small placeholder tree and offloads the old tree to a background thread, which is a strong sign this is snapshot-persistent state 
   
* crates/multi\_buffer/src/path\_key.rs  
  * MultiBuffer snapshots hold SumTree\-backed excerpt/path indexes  
  * the code rebuilds tree snapshots incrementally as excerpts change  
  
* crates/editor/src/display\_map/\*  
  * FoldSnapshot, InlaySnapshot, CreaseSnapshot, WrapSnapshot, etc. all store SumTrees inside snapshot structs  
  * these snapshots are cloned and reused as the display changes  
  
* crates/project/src/git\_store/diff\_buffer\_list.rs  
  * statuses\_by\_path: Option\<SumTree\<StatusEntry\>\>  
  * tree-backed status lists are retained across updates

### The key idea

Zed doesn’t usually “serialize the tree to disk.”  
Instead, it persists the logical state that contains the tree, and the tree itself stays shared and immutable-ish via Arc, with mutations producing updated snapshots.

### Most relevant code paths to inspect

If you want the exact places where this happens, start with:

* crates/text/src/text.rs  
  especially the BufferSnapshot / fragment tree code and FragmentBuilder::to\_sum\_tree  
* crates/language/src/syntax\_map.rs  
  SyntaxSnapshot  
* crates/editor/src/display\_map/{fold\_map,inlay\_map,crease\_map,wrap\_map}.rs  
* crates/multi\_buffer/src/path\_key.rs  
* crates/project/src/git\_store/diff\_buffer\_list.rs

### One important nuance

If by “persists” you mean serialization/deserialization to disk, I didn’t find SumTree being directly serde-persisted as a generic type. It’s mainly used as an internal persistent snapshot structure, not a file format.

If you want, I can next trace one concrete tree instance end-to-end, like:

* text::BufferSnapshot’s fragment tree,  
* SyntaxSnapshot.layers,  
* or WrapSnapshot.transforms.
