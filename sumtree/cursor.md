cursor.rs is the navigation and extraction layer for SumTree.

In practical terms, it gives the crate its main read-side API:

* walk through a tree efficiently  
  * move forward/backward item by item  
  * inspect the current item, previous item, next item  
  * maintain the current position in a chosen Dimension 
   
* seek by summary/dimension  
  * jump to a logical location like “byte offset 120”, “line 42”, or any custom dimension  
  * this is what makes SumTree useful for ropes, buffers, diagnostics, and other indexed structures  
  
* slice subtrees without flattening  
  * cursor.slice(...) returns a SumTree containing the traversed range  
  * cursor.suffix() gets the remainder  
  * cursor.summary(...) computes aggregate dimensions over a range 
   
* filter traversal  
  * FilterCursor wraps a normal cursor and skips nodes whose summaries don’t match a predicate  
  * used for things like “iterate only over matching regions”  
  
* support tree iteration  
  * Iter is the internal in-order iterator implementation built on the same traversal machinery

So sum_tree.rs defines the data structure and mutation algorithms, while cursor.rs defines how callers read, seek, slice, and iterate through that structure.

A useful mental model:

* SumTree \= storage \+ balancing \+ edits  
* cursor.rs \= traversal cursor \+ range extraction \+ summary-based seeking

&nbsp;

&nbsp;

&nbsp;

---

&nbsp;

&nbsp;

Sure — here’s the role of the main types in crates/sum\_tree/src/cursor.rs, one by one.

## Cursor\<'a, 'b, T, D\>

This is the main workhorse.

It represents a position inside a SumTree\<T\> and lets you move around while keeping track of a logical coordinate D derived from the tree’s summaries.

### What it stores

* a reference to the tree  
* a stack of nodes along the current path  
* the current logical position (position: D)  
* whether it has already sought  
* whether it is at the end  
* the summary context (cx)

### What it’s for

* seek(...) to jump to a target location  
* next() / prev() to move item by item  
* item() to read the current item  
* prev\_item() / next\_item() to inspect neighbors  
* slice(...) to extract a subtree range  
* summary(...) to compute an aggregate over a range

### In short

Cursor is the API you use when you want to navigate the tree without flattening it.

---

## FilterCursor\<'a, 'b, F, T, U\>

This is a cursor wrapper that skips items based on a predicate over summaries.

It wraps a normal Cursor and a predicate like:

Rust

FnMut(\&T::Summary) \-\> bool

&nbsp;

### What it’s for

* iterate only over items/nodes whose summaries match some condition  
* efficiently skip irrelevant parts of the tree  
* useful for things like “find visible items”, “only even-numbered regions”, or “only nodes that overlap a condition”

### How it behaves

* next() advances to the next matching item  
* prev() moves backward to the previous matching item  
* item() and start() are forwarded to the underlying cursor

### In short

FilterCursor is for filtered traversal.

---

## Iter\<'a, T\>

This is the crate’s in-order iterator over a SumTree\<T\>.

### What it’s for

* standard Rust iteration over all items in tree order  
* used by SumTree::iter()

### Why it exists separately

A cursor is a stateful navigation object that can seek and move in both directions.  
Iter is the simpler one-way iterator abstraction built on the same traversal logic.

### In short

Iter is the plain iterator view of the tree.

---

## StackEntry\<'a, T, D\>

This is an internal helper type used by cursor traversal.

You won’t normally use it directly.

### What it represents

One frame on the traversal stack:

* which subtree you’re in  
* which child index you’re at  
* enough state to resume traversal after moving down/up the tree

### Why it matters

The cursor doesn’t recurse recursively at runtime; it keeps an explicit stack.  
That makes movement efficient and avoids recursion overhead.

### In short

StackEntry is the breadcrumb the cursor uses to remember where it is.

---

## SeekAggregate\<'a, T\>

This is an internal trait for collecting results during seeking.

It defines hooks like:

* begin\_leaf()  
* end\_leaf(...)  
* push\_item(...)  
* push\_tree(...)

### What it’s for

It lets the same seek traversal logic power different outcomes:

* build a sliced subtree  
* compute a summary across a range  
* possibly other specialized traversals

### In short

SeekAggregate is the callback interface for range traversal.

---

## SliceSeekAggregate\<T\>

This is one concrete implementation of SeekAggregate.

### What it does

It collects traversed items into a brand-new SumTree\<T\> slice.

### Why it exists

Cursor::slice(...) needs to walk from the current position to a target and build a tree representing that range.  
This type holds the in-progress result while traversal runs.

### In short

SliceSeekAggregate is the builder used by cursor.slice().

---

## SummarySeekAggregate\<D\>

This is the other main SeekAggregate implementation.

### What it does

It accumulates a Dimension value while traversing a range.

### Why it exists

Cursor::summary(...) computes the aggregate logical position/dimension over a range without returning the items themselves.

### In short

SummarySeekAggregate is the collector used by cursor.summary().

---

## How they fit together

* Cursor \= the main traversal state  
* FilterCursor \= Cursor with a predicate  
* Iter \= one-way iteration over a tree  
* StackEntry \= internal traversal state  
* SeekAggregate \= internal traversal output interface  
* SliceSeekAggregate \= builds a sliced tree  
* SummarySeekAggregate \= computes aggregate dimensions
