

### Where is the foreground executor used ?

- zed.rs: *fn about*

```rust
let prompt = cx.prompt(PromptLevel::Info, &message, detail.as_deref(), &["OK"]);

cx.foreground_executor()
    .spawn(async {
        prompt.await.ok();
    })
    .detach();
```

- workspace.rs: *pub fn split_pane_with_project_entry*

```rust
let task = self.open_path(path, Some(new_pane.downgrade()), true, cx);
Some(cx.foreground_executor().spawn(async move {
     task.await?;
     Ok(())
 }))
```

### References

- [std::sync::mpsc](https://doc.rust-lang.org/std/sync/mpsc/index.html)
