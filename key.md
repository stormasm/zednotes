
_For newer notes on this subject see [keymap.md](./keymap.md)_

### Make this println! addition to key_dispatch.rs

This will then print out each time you hit a key along with the modifiers.

- [key_dispatch branch](https://github.com/stormasm/zed/tree/key_dispatch)
- [key_dispatch.rs](https://github.com/zed-industries/zed/blob/main/crates/gpui/src/key_dispatch.rs)

```rust
pub fn dispatch_key(
    &mut self,
    mut input: SmallVec<[Keystroke; 1]>,
    keystroke: Keystroke,
    dispatch_path: &SmallVec<[DispatchNodeId; 32]>,
) -> DispatchResult {
    println!("dispatch_key {:?}", keystroke);
    input.push(keystroke.clone());
    let (bindings, pending) = self.bindings_for_input(&input, dispatch_path);
```

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

### Debugging details of the problem

```rust
fn dispatch_action_on_node(&mut self, node_id: DispatchNodeId, action: &dyn Action) {
    let dispatch_path = self
        .window
        .rendered_frame
        .dispatch_tree
        .dispatch_path(node_id);

    println!("dispatch_action_on_node: {:?}", action);
```

### bindings_for_action

There is a test in *zed.rs* that probably sheds a lot more light on this topic.

```rust
    fn assert_key_bindings_for(
```

### node_id & dispatch_path inside dispatch_key_event

```rust
    fn dispatch_key_event(&mut self, event: &dyn Any) {
        println!("dispatch_key_event {:?}", std::time::SystemTime::now());
        if self.window.dirty.get() {
            self.draw();
        }

        let node_id = self
            .window
            .focus
            .and_then(|focus_id| {
                self.window
                    .rendered_frame
                    .dispatch_tree
                    .focusable_node_id(focus_id)
            })
            .unwrap_or_else(|| self.window.rendered_frame.dispatch_tree.root_node_id());

        println!("node_id {:?}", node_id);

        let dispatch_path = self
            .window
            .rendered_frame
            .dispatch_tree
            .dispatch_path(node_id);

        println!("dispatch_path {:?}", dispatch_path);
```

- [key_dispatch.rs](https://github.com/zed-industries/zed/blob/main/crates/gpui/src/key_dispatch.rs) contains the method *dispatch_key*

```rust
if let Some(key_down_event) = event.downcast_ref::<KeyDownEvent>() {
     let KeymatchResult { bindings, pending } = self
         .window
         .rendered_frame
         .dispatch_tree
         .dispatch_key(&key_down_event.keystroke, &dispatch_path);

     println!("bindings: {:?}", bindings);
     println!("pending: {:?}", pending);
```

- [storybook keybinding](https://github.com/zed-industries/zed/blob/main/crates/ui/src/key_bindings.rs)

### Reference

- [Bubbling and capturing](https://javascript.info/bubbling-and-capturing)
