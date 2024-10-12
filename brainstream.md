
### implement Trait on the type [or struct]

```rust
rg "impl Element for"
```

### view.rs

```rust
impl Element for AnyView {
```

### element.rs

```rust
/// Implemented by types that participate in laying out and painting the contents of a window.
/// Elements form a tree and are laid out according to web-based layout rules, as implemented by Taffy.
/// You can create custom elements by implementing this trait, see the module-level documentation
/// for more details.
pub trait Element: 'static + IntoElement {


/// Implemented by any type that can be converted into an element.
pub trait IntoElement: Sized {

/// An object that can be drawn to the screen. This is the trait that distinguishes `Views` from
/// models. Views are drawn to the screen and care about the current window's state, models are not and do not.
pub trait Render: 'static + Sized {
    /// Render this view into an element tree.
    fn render(&mut self, cx: &mut ViewContext<Self>) -> impl IntoElement;
}

/// You can derive [`IntoElement`] on any type that implements this trait.
/// It is used to construct reusable `components` out of plain data. Think of
/// components as a recipe for a certain pattern of elements. RenderOnce allows
/// you to invoke this pattern, without breaking the fluent builder pattern of
/// the element APIs.
pub trait RenderOnce: 'static {
    /// Render this component into an element tree. Note that this method
    /// takes ownership of self, as compared to [`Render::render()`] method
    /// which takes a mutable reference.
    fn render(self, cx: &mut WindowContext) -> impl IntoElement;
}
```

### structs

```rust
/// A view is a piece of state that can be presented on screen by implementing the [Render] trait.
/// Views implement [Element] and can composed with other views, and every window is created with a root view.
pub struct View<V> {
    /// A view is just a [Model] whose type implements `Render`, and the model is accessible via this field.
    pub model: Model<V>,
}

/// A dynamically-typed handle to a view, which can be downcast to a [View] for a specific type.
#[derive(Clone, Debug)]
pub struct AnyView {
    model: AnyModel,
    render: fn(&AnyView, &mut WindowContext) -> AnyElement,
    cached_style: Option<StyleRefinement>,
}


/// A dynamically typed element that can be used to store any element type.
pub struct AnyElement(ArenaBox<dyn ElementObject>);

```

---

### Understand `EventEmitter` in gpui specifically the files:

- window.rs
- app.rs
- model_context.rs
- test_context.rs

---

rg "emit\("

#### Understand how the pub / sub system works

- starting with `emit`
- loop

```rust
/// Emit an event to be handled by any other views that have subscribed via [ViewContext::subscribe].
pub fn emit<Evt>(&mut self, event: Evt)
where
    Evt: 'static,
    V: EventEmitter<Evt>,
{
    let emitter = self.view.model.entity_id;
    self.app.push_effect(Effect::Emit {
        emitter,
        event_type: TypeId::of::<Evt>(),
        event: Box::new(event),
    });
}
```

rg SubscriberSet

---

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
