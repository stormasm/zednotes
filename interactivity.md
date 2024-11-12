
To get interactivity going on any `interactive` div type including

- Button
- Tab
- ResizeHandle

in `gpui-component` for example simply

```rust
impl InteractiveElement for Button {
    fn interactivity(&mut self) -> &mut gpui::Interactivity {
        self.base.interactivity()
    }
}
```

##### div.rs

```rust
pub struct Interactivity
pub trait InteractiveElement
```

##### window.rs

```rust
pub enum ElementId
```

### References

- [pub enum ElementId](https://github.com/zed-industries/zed/blob/main/crates/gpui/src/window.rs#L4841)
- [pub struct Interactivity](https://github.com/zed-industries/zed/blob/main/crates/gpui/src/elements/div.rs#L1240)
- [pub trait InteractiveElement](https://github.com/zed-industries/zed/blob/main/crates/gpui/src/elements/div.rs#L520)
