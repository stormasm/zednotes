

in `gpui` try to understand better how to track the focus or know what is focused at the moment

rg FocusHandle

---

come up to speed on slotmap in the context of FocusId

slotmap::new_key_type! {
    /// A globally unique identifier for a focusable element.
    pub struct FocusId;
}

---

in the `tab_switcher` comment out this line of code or any other object that implements `ModalView`

```rust
impl ModalView for TabSwitcher {}
```

So I can begin to understand

```rust
workspace.toggle_modal
```

---

rg observe_new_views

this is where the `move |workspace: &mut Workspace, cx|` happens !

```rust
pub fn initialize_workspace(
    app_state: Arc<AppState>,
    prompt_builder: Arc<PromptBuilder>,
    cx: &mut AppContext,
) {
    cx.observe_new_views(move |workspace: &mut Workspace, cx| {
        let workspace_handle = cx.view().clone();
        let center_pane = workspace.active_pane().clone();
        initialize_pane(workspace, &center_pane, cx);
```
