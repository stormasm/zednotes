
#### crates/workspace/src/pane.rs

```rust
impl Render for Pane {
    fn render(&mut self, cx: &mut ViewContext<Self>) -> impl IntoElement {
        let mut key_context = KeyContext::new_with_defaults();
        key_context.add("Pane");
        if self.active_item().is_none() {
            key_context.add("EmptyPane");
        }

        cx.bind_keys([KeyBinding::new("cmd-w", CloseActiveItem, Some("Pane"))]);

        let should_display_tab_bar = self.should_display_tab_bar.clone();
        let display_tab_bar = should_display_tab_bar(cx);
```
