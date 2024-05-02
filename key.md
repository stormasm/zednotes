
### Documentation

- [Key Dispatch](https://github.com/zed-industries/zed/blob/main/crates/gpui/docs/key_dispatch.md)

#### gpui/src/window.rs

```rust
fn dispatch_key_event(&mut self, event: &dyn Any) {
```

- This is similar to [crossterm's event-read.rs](https://github.com/crossterm-rs/crossterm/blob/master/examples/event-read.rs)
- And you can see stuff in storybook's [focus.rs](https://github.com/zed-industries/zed/blob/main/crates/storybook/src/stories/focus.rs) where it goes ahead and prints the key events.
