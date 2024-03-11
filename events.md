
### The gpui Event System

##### gpui.rs

```rust
/// A trait for tying together the types of a GPUI entity and the events it can emit
pub trait EventEmitter<E: Any>: 'static {}
```

##### window.rs

- [pub fn emit](https://github.com/zed-industries/zed/blob/main/crates/gpui/src/window.rs#L2229)

##### app.rs

- [pub fn subscribe](https://github.com/zed-industries/zed/blob/main/crates/gpui/src/app.rs#L410)

##### References

- [ownership_post.rs](https://github.com/zed-industries/zed/blob/main/crates/gpui/examples/ownership_post.rs)
