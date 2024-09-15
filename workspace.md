
- [What is an Item and a Pane ?](./item.md)
- [More details on the Pane](./pane.md)

### Top Level Flow for Workspaces

| Key Binding | Action | Command Palette |
| ----------- | ------ | --------------- |
| cmd-shift-n | workspace::NewWindow | workspace: new window
| cmd-o | workspace::Open | workspace: open


The editor gets initialized the first time
Zed gets fired up... The *on_action* for *NewWindow* is defined so that
every time someone triggers the keystroke which fires
a *NewWindow* it goes to the editor code
which in turn calls into the workspace code *open_new*.

##### editor.rs

```rust
cx.on_action(move |_: &workspace::NewWindow, cx| {
    let app_state = workspace::AppState::global(cx);
    if let Some(app_state) = app_state.upgrade() {
        workspace::open_new(app_state, cx, |workspace, cx| {
            Editor::new_file(workspace, &Default::default(), cx)
        })
        .detach();
    }
});
```

Note that the on_actions for both *NewFile* and *NewWindow* in the editor
the code is identical yet in the *open_new* code below its the
*opened_paths.is_empty()* which drives whether a new Item (see below) shows up in
the editor or a new workspace window gets init'ed.


##### main.rs

```rust
async fn restore_or_create_workspace(
    app_state: Arc<AppState>,
    cx: &mut AsyncAppContext,
) -> Result<()> {
    if let Some(locations) = restorable_workspace_locations(cx, &app_state).await {
        for location in locations {
            cx.update(|cx| {
                workspace::open_paths(
                    location.paths().as_ref(),
                    app_state.clone(),
                    workspace::OpenOptions::default(),
                    cx,
                )
            })?
            .await?;
        }
    } else if matches!(KEY_VALUE_STORE.read_kvp(FIRST_OPEN), Ok(None)) {
        cx.update(|cx| show_welcome_view(app_state, cx))?.await?;
    } else {
        cx.update(|cx| {
            workspace::open_new(Default::default(), app_state, cx, |workspace, cx| {
                Editor::new_file(workspace, &Default::default(), cx)
            })
        })?
        .await?;
    }

    Ok(())
}
```

##### workspace.rs

```rust
pub fn open_new(
    app_state: Arc<AppState>,
    cx: &mut AppContext,
    init: impl FnOnce(&mut Workspace, &mut ViewContext<Workspace>) + 'static + Send,
) -> Task<anyhow::Result<()>> {
    let task = Workspace::new_local(Vec::new(), app_state, None, cx);
    cx.spawn(|mut cx| async move {
        let (workspace, opened_paths) = task.await?;
        workspace.update(&mut cx, |workspace, cx| {
            if opened_paths.is_empty() {
                init(workspace, cx)
            }
        })?;
        Ok(())
    })
}
```

### Pane

This is the data structure that tabs or items live in. So when you are looking at the editor in Zed each tab that you see at the top of the screen is associated with an Item.

A Pane has a vector of Items.

### PaneGroup

This has to do with splitting the panes and it has an axis associated with it.
