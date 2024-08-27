
##### kallax, gpui-calculator, hello-world

```rust
App::new().run(|cx| {})
```

##### loungy

```rust
App:new();
run_app(app)
```

##### zed, gpui-component

```rust
let app = App::new().with_assets(Assets);
app.run(move |cx| {})
```

##### zed workspace.rs

*open_new* calls into *new_local*

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
            workspace::open_new(app_state, cx, |workspace, cx| {
                Editor::new_file(workspace, &Default::default(), cx)
            })
        })?
        .await?;
    }

    Ok(())
}
```
