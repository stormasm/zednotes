
### The gpui Event System

##### gpui.rs

```rust
/// A trait for tying together the types of a GPUI entity and the events it can emit
pub trait EventEmitter<E: Any>: 'static {}
```

##### window.rs

- [pub fn emit](https://github.com/zed-industries/zed/blob/main/crates/gpui/src/window.rs#L2229)

##### app.rs

```
/// These effects are processed at the end of each application update cycle.
pub(crate) enum Effect {
    Notify {
        emitter: EntityId,
    },
    Emit {
        emitter: EntityId,
        event_type: TypeId,
        event: Box<dyn Any>,
    },
    Refresh,
    NotifyGlobalObservers {
        global_type: TypeId,
    },
    Defer {
        callback: Box<dyn FnOnce(&mut AppContext) + 'static>,
    },
}
```

- [pub fn subscribe](https://github.com/zed-industries/zed/blob/main/crates/gpui/src/app.rs#L410)

##### References

- [ownership_post.rs](https://github.com/zed-industries/zed/blob/main/crates/gpui/examples/ownership_post.rs)
