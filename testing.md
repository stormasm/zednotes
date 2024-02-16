

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

### Notes on ways to test Zed

* [gpui_macros.rs](https://github.com/zed-industries/zed/blob/main/crates/gpui_macros/src/gpui_macros.rs)
