
* [Start here](https://github.com/zed-industries/zed/blob/main/crates/gpui/docs/contexts.md)


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
