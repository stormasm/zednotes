
#### element.rs

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

#### gpui.rs

```rust
/// A trait for tying together the types of a GPUI entity and the events it can
/// emit.
pub trait EventEmitter<E: Any>: 'static {}
```

#### window.rs

```rust
/// FocusableView allows users of your view to easily
/// focus it (using cx.focus_view(view))
pub trait FocusableView: 'static + Render {
    /// Returns the focus handle associated with this view.
    fn focus_handle(&self, cx: &AppContext) -> FocusHandle;
}
```
