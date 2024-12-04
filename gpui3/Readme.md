
- working off this [branch](https://github.com/zed-industries/zed/compare/main...gpui3)

##### window.rs

- remove `pub struct ViewContext`
- remove `pub struct WindowContext`

and completely remove the file `view.rs`

---

#### When does the file "view.rs" get removed from the code ?

On Nov 24 `view.rs` is removed here with the comment `WIP`   
It is the first `WIP` after `Checkpoint`
```rust   
e28104b2e8b2f7649137dd81411435d02d577be4
```
