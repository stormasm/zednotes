
### Summary

* ModelContext is AppContext & a Model
* WindowContext is AppContext & a Window
* ViewContext is WindowContext & a View
* Window has a root View
* View has a Model

```
     AppContext
     /        \
ModelContext  WindowContext
              /
        ViewContext
```

##### Only one AppContext gets instantiated per application

impl AppContext {
    #[allow(clippy::new_ret_no_self)]
    pub(crate) fn new(
        platform: Rc<dyn Platform>,
        asset_source: Arc<dyn AssetSource>,
        http_client: Arc<dyn HttpClient>,
    ) -> Rc<AppCell> {
        println!("AppContext::new");
        let executor = platform.background_executor();
        let foreground_executor = platform.foreground_executor();
        assert!(
            executor.is_main_thread(),
            "must construct App on main thread"
        );


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

##### window.rs

```rust
/// Provides access to application state in the context of a single window. Derefs
/// to an [`AppContext`], so you can also pass a [`WindowContext`] to any method that takes
/// an [`AppContext`] and call any [`AppContext`] methods.
pub struct WindowContext<'a> {
    pub(crate) app: &'a mut AppContext,
    pub(crate) window: &'a mut Window,
}

/// Provides access to application state that is specialized for a particular [`View`].
/// Allows you to interact with focus, emit events, etc.
/// ViewContext also derefs to [`WindowContext`], giving you access to all of its methods as well.
/// When you call [`View::update`], you're passed a `&mut V` and an `&mut ViewContext<V>`.
pub struct ViewContext<'a, V> {
    window_cx: WindowContext<'a>,
    view: &'a View<V>,
}
```

##### app/entity_map.rs

```rust
/// A strong, well typed reference to a struct which is managed
/// by GPUI
#[derive(Deref, DerefMut)]
pub struct Model<T> {
    #[deref]
    #[deref_mut]
    pub(crate) any_model: AnyModel,
    pub(crate) entity_type: PhantomData<T>,
}
```

##### window.rs

```rust
// Holds the state for a specific window.
#[doc(hidden)]
pub struct Window {
    pub(crate) root_view: Option<AnyView>,
    ...
```

##### view.rs

```rust
/// A view is a piece of state that can be presented on screen by implementing the [Render] trait.
/// Views implement [Element] and can composed with other views, and every window is created with a root view.
pub struct View<V> {
    /// A view is just a [Model] whose type implements `Render`, and the model is accessible via this field.
    pub model: Model<V>,
}
```

##### gpui.rs -> all of the Contexts are *structs* except for these two *traits*

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

##### app.rs

```rust
/// Contains the state of the full application, and passed as a reference to a variety of callbacks.
/// Other contexts such as [ModelContext], [WindowContext], and [ViewContext] deref to this type,
/// making it the most general context type.
/// You need a reference to an `AppContext` to access the state of a [Model].
pub struct AppContext {
    pub(crate) this: Weak<AppCell>,
    pub(crate) platform: Rc<dyn Platform>,
    app_metadata: AppMetadata,
    text_system: Arc<TextSystem>,
    flushing_effects: bool,
    pending_updates: usize,
    pub(crate) actions: Rc<ActionRegistry>,
    pub(crate) active_drag: Option<AnyDrag>,
    pub(crate) background_executor: BackgroundExecutor,
    pub(crate) foreground_executor: ForegroundExecutor,
    pub(crate) svg_renderer: SvgRenderer,
    asset_source: Arc<dyn AssetSource>,
    pub(crate) image_cache: ImageCache,
    pub(crate) text_style_stack: Vec<TextStyleRefinement>,
    pub(crate) globals_by_type: FxHashMap<TypeId, Box<dyn Any>>,
    pub(crate) entities: EntityMap,
    pub(crate) new_view_observers: SubscriberSet<TypeId, NewViewListener>,
    pub(crate) windows: SlotMap<WindowId, Option<Window>>,
    pub(crate) window_handles: FxHashMap<WindowId, AnyWindowHandle>,
    pub(crate) keymap: Rc<RefCell<Keymap>>,
    pub(crate) global_action_listeners:
        FxHashMap<TypeId, Vec<Rc<dyn Fn(&dyn Any, DispatchPhase, &mut Self)>>>,
    pending_effects: VecDeque<Effect>,
    pub(crate) pending_notifications: FxHashSet<EntityId>,
    pub(crate) pending_global_notifications: FxHashSet<TypeId>,
    pub(crate) observers: SubscriberSet<EntityId, Handler>,
    // TypeId is the type of the event that the listener callback expects
    pub(crate) event_listeners: SubscriberSet<EntityId, (TypeId, Listener)>,
    pub(crate) keystroke_observers: SubscriberSet<(), KeystrokeObserver>,
    pub(crate) release_listeners: SubscriberSet<EntityId, ReleaseListener>,
    pub(crate) global_observers: SubscriberSet<TypeId, Handler>,
    pub(crate) quit_observers: SubscriberSet<(), QuitHandler>,
    pub(crate) layout_id_buffer: Vec<LayoutId>, // We recycle this memory across layout requests.
    pub(crate) propagate_event: bool,
}
```

### References

* [contexts.md](https://github.com/zed-industries/zed/blob/main/crates/gpui/docs/contexts.md)
