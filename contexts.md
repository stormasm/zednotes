
* [Start here](https://github.com/zed-industries/zed/blob/main/crates/gpui/docs/contexts.md)

##### gpui.rs
```rust
/// The context trait, allows the different contexts in GPUI to be used
/// interchangeably for certain operations.
pub trait Context {
    /// The result type for this context, used for async contexts that
    /// can't hold a direct reference to the application context.
    type Result<T>;

    /// Create a new model in the app context.
    fn new_model<T: 'static>(
        &mut self,
        build_model: impl FnOnce(&mut ModelContext<'_, T>) -> T,
    ) -> Self::Result<Model<T>>;

    /// Update a model in the app context.
    fn update_model<T, R>(
        &mut self,
        handle: &Model<T>,
        update: impl FnOnce(&mut T, &mut ModelContext<'_, T>) -> R,
    ) -> Self::Result<R>
    where
        T: 'static;

    /// Read a model from the app context.
    fn read_model<T, R>(
        &self,
        handle: &Model<T>,
        read: impl FnOnce(&T, &AppContext) -> R,
    ) -> Self::Result<R>
    where
        T: 'static;

    /// Update a window for the given handle.
    fn update_window<T, F>(&mut self, window: AnyWindowHandle, f: F) -> Result<T>
    where
        F: FnOnce(AnyView, &mut WindowContext<'_>) -> T;

    /// Read a window off of the application context.
    fn read_window<T, R>(
        &self,
        window: &WindowHandle<T>,
        read: impl FnOnce(View<T>, &AppContext) -> R,
    ) -> Result<R>
    where
        T: 'static;
}

/// This trait is used for the different visual contexts in GPUI that
/// require a window to be present.
pub trait VisualContext: Context {
    /// Construct a new view in the window referenced by this context.
    fn new_view<V>(
        &mut self,
        build_view: impl FnOnce(&mut ViewContext<'_, V>) -> V,
    ) -> Self::Result<View<V>>
    where
        V: 'static + Render;

    /// Update a view with the given callback
    fn update_view<V: 'static, R>(
        &mut self,
        view: &View<V>,
        update: impl FnOnce(&mut V, &mut ViewContext<'_, V>) -> R,
    ) -> Self::Result<R>;

    /// Replace the root view of a window with a new view.
    fn replace_root_view<V>(
        &mut self,
        build_view: impl FnOnce(&mut ViewContext<'_, V>) -> V,
    ) -> Self::Result<View<V>>
    where
        V: 'static + Render;

    /// Focus a view in the window, if it implements the [`FocusableView`] trait.
    fn focus_view<V>(&mut self, view: &View<V>) -> Self::Result<()>
    where
        V: FocusableView;

    /// Dismiss a view in the window, if it implements the [`ManagedView`] trait.
    fn dismiss_view<V>(&mut self, view: &View<V>) -> Self::Result<()>
    where
        V: ManagedView;
}
```


##### app/model_context.rs
```rust
/// The app context, with specialized behavior for the given model.
#[derive(Deref, DerefMut)]
pub struct ModelContext<'a, T> {
    #[deref]
    #[deref_mut]
    app: &'a mut AppContext,
    model_state: WeakModel<T>,
}
```
