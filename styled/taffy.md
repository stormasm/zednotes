
- [element.rs doc about Taffy and Layout](https://github.com/zed-industries/zed/blob/main/crates/gpui/src/element.rs)

The *TaffyLayoutEngine* is mainly just referenced in

- crates/gpui/src/window.rs
- crates/gpui/src/element.rs

---

```rust
zed$ rg compute_layout
crates/gpui/src/taffy.rs
146:    pub fn compute_layout(
182:            .compute_layout_with_measure(
201:        // println!("compute_layout took {:?}", started_at.elapsed());

crates/gpui/src/element.rs
499:                window.compute_layout(layout_id, available_space, cx);
517:                    window.compute_layout(layout_id, available_space, cx);

crates/gpui/src/window.rs
3017:    pub fn compute_layout(
3026:        layout_engine.compute_layout(layout_id, available_space, self, cx);
```
