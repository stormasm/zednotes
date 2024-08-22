
- [View](https://github.com/zed-industries/zed/blob/main/crates/gpui/src/view.rs)

A view is a piece of state that can be presented on screen by implementing the [Render] trait.   
Views implement [Element] and can composed with other views, and every window is created with a root view.   
A view is just a [Model] whose type implements `Render`, and the model is accessible via this field.
