
#### PanelHandle

```rust
pub trait PanelHandle: Send + Sync {
```

#### Other notes

To see whats going on with `dock` go to the workspace crate.

First thing to do in the workspace crate is to

```
rg resize
```

And you will see that this is dealt with in

- dock.rs
- pane_group.rs
- workspace.rs
