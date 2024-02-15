
### Single Line Editor Concepts in Zed

Here is the code *editor.rs*

```rust
impl Editor {
    pub fn single_line(cx: &mut ViewContext<Self>) -> Self {
        let buffer = cx.new_model(|cx| {
            Buffer::new(
                0,
                BufferId::new(cx.entity_id().as_u64()).unwrap(),
                String::new(),
            )
        });
        let buffer = cx.new_model(|cx| MultiBuffer::singleton(buffer, cx));
        Self::new(EditorMode::SingleLine, buffer, None, cx)
    }
```

This is how you can reference it

```rust
Editor::single_line
```
