
### cx.focus_view
- Research this subject more :)

- rg "impl ModalView for"
- rg toggle_modal

##### workspace.rs

```rust
pub fn toggle_modal<V: ModalView, B>(&mut self, cx: &mut WindowContext, build: B)
```

##### modal_layer.rs

```rust
option command O

crates/recent_projects/src/recent_projects.rs
65:impl ModalView for RecentProjects {}

option command B

crates/vcs_menu/src/lib.rs
55:impl ModalView for BranchList {}

command P

crates/file_finder/src/file_finder.rs
35:impl ModalView for FileFinder {}

Ctrl Tab

crates/tab_switcher/src/tab_switcher.rs
37:impl ModalView for TabSwitcher {}

Ctrl g

crates/go_to_line/src/go_to_line.rs
29:impl ModalView for GoToLine {}

cmd k cmd t

crates/theme_selector/src/theme_selector.rs
51:impl ModalView for ThemeSelector {}

Cmd Shift P

crates/command_palette/src/command_palette.rs
35:impl ModalView for CommandPalette {}
```
