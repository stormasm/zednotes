
### picker.rs

```rust
fn on_input_editor_event(
    &mut self,
    _: View<Editor>,
    event: &editor::EditorEvent,
    cx: &mut ViewContext<Self>,
) {
```

on_input_editor_event is NEVER being called when you hit the backspace key


```rust
let now = std::time::SystemTime::now();
println!("{:?}",now);
```

- EditorMode::SingleLine
- Editor::single_line(cx);
- EditorEvent

### Issues

editor/src/editor.rs

```rust
pub fn backspace(&mut self, _: &Backspace, cx: &mut ViewContext<Self>) {
     println!("editor backspace");
     self.transact(cx, |this, cx| {
```

backspace is not being fired on storybook picker

editor/src/element.rs calls

```rust
register_action(view, cx, Editor::backspace);
```

### Examples

- file_finder
- theme_selector
- welcome: toggle base keymap theme_selector

```rust
rg 'impl PickerDelegate for '
```

```rust
rg Editor::single_line
```

```rust
rg Picker::uniform_list
```
