

### Model Examples to Understand Zed Tests

* [workspace/src/pane.rs](https://github.com/zed-industries/zed/blob/main/crates/workspace/src/pane.rs#L2095)

```rust
#[gpui::test]
    async fn test_close_items_to_the_right(cx: &mut TestAppContext) {
        init_test(cx);
        let fs = FakeFs::new(cx.executor());

        let project = Project::test(fs, None, cx).await;
        let (workspace, cx) = cx.add_window_view(|cx| Workspace::test_new(project.clone(), cx));
        let pane = workspace.update(cx, |workspace, _| workspace.active_pane().clone());

        set_labeled_items(&pane, ["A", "B", "C*", "D", "E"], cx);

        pane.update(cx, |pane, cx| {
            pane.close_items_to_the_right(&CloseItemsToTheRight, cx)
        })
        .unwrap()
        .await
        .unwrap();
        assert_item_labels(&pane, ["A", "B", "C*"], cx);
    }
```

### Notes on this code

#### gpui/src/app/test_context.rs

```rust
/// Adds a new window, and returns its root view and a `VisualTestContext` which can be used
/// as a `WindowContext` for the rest of the test. Typically you would shadow this context with
/// the returned one. `let (view, cx) = cx.add_window_view(...);`
pub fn add_window_view<F, V>(&mut self, build_window: F) -> (View<V>, &mut VisualTestContext)
where
    F: FnOnce(&mut ViewContext<V>) -> V,
    V: 'static + Render,
{
    let mut cx = self.app.borrow_mut();
    let window = cx.open_window(WindowOptions::default(), |cx| cx.new_view(build_window));
    drop(cx);
    let view = window.root_view(self).unwrap();
    let cx = VisualTestContext::from_window(*window.deref(), self).as_mut();
    cx.run_until_parked();

    // it might be nice to try and cleanup these at the end of each test.
    (view, cx)
}
```

#### gpui/src/view -> update

```rust
/// Updates the view's state with the given function, which is passed a mutable reference and a context.
 pub fn update<C, R>(
     &self,
     cx: &mut C,
     f: impl FnOnce(&mut V, &mut ViewContext<'_, V>) -> R,
 ) -> C::Result<R>
 where
     C: VisualContext,
 {
     cx.update_view(self, f)
 }
```

### Notes on ways to test Zed

* [gpui_macros.rs](https://github.com/zed-industries/zed/blob/main/crates/gpui_macros/src/gpui_macros.rs)
