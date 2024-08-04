
August 2024

For older notes on this subject see [key.md](./key.md)

#### interesting methods in gpui/src/key_dispatch.rs

- [available_actions](https://github.com/zed-industries/zed/blob/main/crates/gpui/src/key_dispatch.rs)
- [used by a test with the function assert_key_bindings for in zed.rs](https://github.com/zed-industries/zed/blob/main/crates/zed/src/zed.rs)
- [used by the command_palette.rs](https://github.com/zed-industries/zed/blob/main/crates/command_palette/src/command_palette.rs)

#### handle_keymap_file_changes

in zed/src/main.rs is a method called *handle_keymap_file_changes*

which calls into

crates/zed/src/zed.rs

where the method is located and implemented.
