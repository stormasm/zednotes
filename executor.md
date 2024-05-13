

### Where is the foreground executor used ?

Simply run the command

```rust
rg foreground_executor
```

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

- project_panel.rs: *fn move_entry*

```rust
let task = project.rename_entry(entry_to_move, new_path, cx);
cx.foreground_executor().spawn(task).detach_and_log_err(cx);
```

### References

- [std::sync::mpsc](https://doc.rust-lang.org/std/sync/mpsc/index.html)
