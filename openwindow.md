
### How does open_window happen in Zed

#### crates/zed/src/main.rs

```rust
- main.rs -> contains the fn main
- which calls -> fn init_ui
- main.rs -> init_ui contains the fn initialize_workspace
- which gets called
- main.rs -> init_ui contains the fn restore_or_create_workspace
- which calls -> fn workspace::open_new
```

#### crates/zed/src/zed.rs

```rust
- main()
- init_ui
- initialize_workspace
- initialize_pane
```

#### crates/workspace/src/workspace.rs

```rust
- workspace.rs contains open_new
- which calls -> fn Workspace::new_local
- workspace.rs contains new_local
- which calls -> fn cx.open_window
```

#### crates/gpui/src/app.rs

```rust
- app.rs -> contains the fn open_window
- which calls -> fn Window::new
```

#### crates/gpui/src/window.rs

```rust
- window.rs -> contains the fn Window:new
- which calls -> fn dispatch_event
- window.rs contains the fn dispatch_event
- which calls -> fn dispatch_key_event and fn dispatch_mouse_event
```
