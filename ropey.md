
### Core Design

- B-tree Structure: It uses a B-tree instead of a traditional strict binary tree to store text chunks.
- Leaf Nodes: Leaves hold text chunks encoded as UTF-8 alongside metadata like character counts and line breaks.
- Branch Nodes: Internal nodes store summaries of child metrics to enable fast random access and indexing. 

---

- [repo: ropey](https://cessen.github.io/ropey/)
- [repo called rope](https://github.com/kavirajk/rope)
- [ropey design](https://github.com/cessen/ropey/blob/master/design/design.md)
