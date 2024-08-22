
- [View](https://github.com/zed-industries/zed/blob/main/crates/gpui/src/view.rs)

A view is a piece of state that can be presented on screen by implementing the [Render] trait.   
Views implement [Element] and can composed with other views, and every window is created with a root view.   
A view is just a [Model] whose type implements `Render`, and the model is accessible via this field.

- [Element](https://github.com/zed-industries/zed/blob/main/crates/gpui/src/element.rs)

Elements are the workhorses of GPUI. They are responsible for laying out and painting all of the contents of a window.
Elements are constructed by calling [`Render::render()`] on the root view of the window, which recursively constructs the element tree from the current state of the application.  These elements are then laid out by Taffy.

[AppContext](https://github.com/zed-industries/zed/blob/main/crates/gpui/src/app.rs)

AppContext contains the state of the full application, and passed as a reference to a variety of callbacks.  Other contexts such as [ModelContext], [WindowContext], and [ViewContext] deref to this type, making it the most general context type. You need a reference to an `AppContext` to access the state of a [Model].
- [Contexts](https://github.com/stormasm/zednotes/blob/main/contexts.md)
