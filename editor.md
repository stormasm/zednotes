
### Single Line Editor Concepts in Zed

Here is the code in *editor.rs*

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

Here is how you can reference it in the codebase...

```rust
Editor::single_line(cx);
```


### Crates that depend on editor

```rust
rg editor.workspace -g Cargo.toml
```

```rust
activity_indicator
assistant
auto_update
breadcrumbs

collab_ui
copilot_ui
diagnostics
extensions_ui

feedback
file_finder
go_to_line
journal

language_selector
language_tools
markdown_preview
outline

picker
project_panel
project_symbols
quick_action_bar

search
storybook
terminal_view
vim
zed
```
