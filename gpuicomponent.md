
### gpui-component branch descriptions

* [gpui-component branches](https://github.com/stormasm/gpui-component/branches/all)
* command_palette2 adds in some more code for an actual command palette to build, but its still not working
* loadkeymap3 is the simple version with just jason's code now that we know the keymap is loading
* loadkeymap2 ties into my zed branch called settings which proves that the keymap file is loading properly
* closeactiveitem shows this code below working

##### crates/workspace/src/pane.rs

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
