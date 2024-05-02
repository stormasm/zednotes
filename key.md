
### Documentation

- [Key Dispatch](https://github.com/zed-industries/zed/blob/main/crates/gpui/docs/key_dispatch.md)
- [Gpui Readme](https://github.com/zed-industries/zed/blob/main/crates/gpui/README.md)

GPUI provides a range of smaller services that are useful for building complex applications:

- Actions are user-defined structs that are used for converting keystrokes into logical operations in your UI. Use this for implementing keyboard shortcuts, such as cmd-q. See the `action` module for more information.

- [interactive.rs](https://github.com/zed-industries/zed/blob/main/crates/gpui/src/interactive.rs)

#### interactive.rs provides the key trait definitions

```rust
/// An event from a platform input source.
pub trait InputEvent: Sealed + 'static {
    /// Convert this event into the platform input enum.
    fn to_platform_input(self) -> PlatformInput;
}

/// A key event from the platform.
pub trait KeyEvent: InputEvent {}

/// A mouse event from the platform.
pub trait MouseEvent: InputEvent {}
```


#### gpui/src/window.rs

```rust
fn dispatch_key_event(&mut self, event: &dyn Any) {
```

- This is similar to [crossterm's event-read.rs](https://github.com/crossterm-rs/crossterm/blob/master/examples/event-read.rs)
- And you can see stuff in storybook's [focus.rs](https://github.com/zed-industries/zed/blob/main/crates/storybook/src/stories/focus.rs) where it goes ahead and prints the key events.
