
rg SubscriberSet

in `gpui` try to understand better how to track the focus or know what is focused at the moment

rg FocusHandle

---

in window.rs `new_view` is how the system wide entities get inserted into Zed.

```rust
impl VisualContext for WindowContext<'_> {
    fn new_view<V>(
        &mut self,
        build_view_state: impl FnOnce(&mut ViewContext<'_, V>) -> V,
    ) -> Self::Result<View<V>>
```

come up to speed on [slotmap](https://docs.rs/slotmap/1.0.7/slotmap/) in the context of FocusId

```rust
slotmap::new_key_type! {
    /// A globally unique identifier for a focusable element.
    pub struct FocusId;
}
```

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

#### Ref Big Goal

Attempting to understand how to get gpui-component modal code to sync up with the way Zed works
so that when I hit a key sequence the modal pops up similar to the way it works in Zed.
In gpui-component I have to double click my mouse in the modal_story prior to the key shortcut
popping up the modal view.

- [branch: keybinding_showmodal_02](https://github.com/stormasm/gpui-component/tree/keybinding_showmodal_02)
