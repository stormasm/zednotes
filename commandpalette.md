
- gpui/src/key_dispatch.rs

```rust
pub fn available_actions(&self, target: DispatchNodeId) -> Vec<Box<dyn Action>> {
     let mut actions = Vec::<Box<dyn Action>>::new();
     ...

     println!("key_dispatch.rs: actions length {}", actions.len());
     actions
 }
```

- where actions length = 348
- so this is indeed all of the stuff in the command_palette
