
August 2024

For older notes on this subject see [key.md](./key.md)

### handle_keymap_file_changes

#### crates/zed/src/main.rs

If you comment out this line of code keymaps do not work, meaning this is
where everything kicks off to get keymaps going...

```rust
handle_keymap_file_changes(user_keymap_file_rx, cx);
```

will also affect *user_keymap_file_rx*

#### crates/zed/src/zed.rs methods affected by commenting out this line include

- reload_keymaps
- load_default_keymap

### open_window

#### gpui/src/app.rs

```rust
/// Opens a new window with the given option and the root view returned by the given function.
 /// The function is invoked with a `WindowContext`, which can be used to interact with window-specific
 /// functionality.
 pub fn open_window<V: 'static + Render>(
```

and from here
```rust
match Window::new(handle.into(), options, cx) {
```

which goes ahead and calls dispatch_event

#### gpui/src/window.rs

```rust
platform_window.on_input({
     let mut cx = cx.to_async();
     Box::new(move |event| {
         handle
             .update(&mut cx, |_, cx| cx.dispatch_event(event))
             .log_err()
             .unwrap_or(DispatchEventResult::default())
     })
 });
```

```rust
pub fn dispatch_event(&mut self, event: PlatformInput) -> DispatchEventResult {
```

calls into *dispatch_key_event*

```rust
platform_window.on_input({
     let mut cx = cx.to_async();
     Box::new(move |event| {
         handle
             .update(&mut cx, |_, cx| cx.dispatch_event(event))
             .log_err()
             .unwrap_or(DispatchEventResult::default())
     })
 });
```

see a simulation / testing scenario with *dispatch_keystroke*

#### interesting methods in gpui/src/key_dispatch.rs

- [available_actions](https://github.com/zed-industries/zed/blob/main/crates/gpui/src/key_dispatch.rs)
- [used by a test with the function assert_key_bindings for in zed.rs](https://github.com/zed-industries/zed/blob/main/crates/zed/src/zed.rs)
- [used by the command_palette.rs](https://github.com/zed-industries/zed/blob/main/crates/command_palette/src/command_palette.rs)
