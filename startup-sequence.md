
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

##### main.rs

The `app.on_reopen` never appears to get kicked off as I never see the message printed when I attempt to add it like this demo code below.

```rust
app.on_reopen(move |cx| {
    println!("zed is starting inside app.on_reopen");

    if let Some(app_state) = AppState::try_global(cx).and_then(|app_state| app_state.upgrade())
    {
        cx.spawn({
            let app_state = app_state.clone();
            |mut cx| async move {
                if let Err(e) = restore_or_create_workspace(app_state, &mut cx).await {
                    fail_to_open_window_async(e, &mut cx)
                }
            }
        })
        .detach();
    }
});
```

*restore_or_create_workspace* calls into *workspace::open_new* calls into *Workspace::new_local*

- [For more details](./workspace.md)

##### zed welcome.rs

- show_wecome_view
