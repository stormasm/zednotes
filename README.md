
### Ripgrep aka rg

```rust
rg 'impl ModalView for '
```

### New Features

- editor: toggle git blame

### logging

- [logging](./logging.md)

#### Imperative vs Declarative

Declarative would be a ui described by implementing Render or RenderOnce and imperative would be described by implementing Element.

The *declarative* API tries to feel web-like, it gives you a flex layout (just like the CSS flexbox) and lets you think about `<div> analogs` and how they fit together.

The *imperative* API is in terms of rectangles,  pixels etc. It lets you define your own concepts and layout algorithms and tries to stay out of the way.

Implementing a raw text editor is just easier with the imperative API. The layouting is relatively simple (just a line of text) and you can model your cursor as an offset into that line

So, using the imperative API is probably a bit easier 😄

[ref 01](https://discord.com/channels/869392257814519848/1217227325217833043/1217283120336998502) <--->
[ref 02](https://discord.com/channels/869392257814519848/1199799855007158352/1217280636222443591)

#### PaneGroup or self.center is the place where the files show up in the workspace

```rust
pub struct Workspace {
    center: PaneGroup
```

Inside the *Render* of workspace.rs

```rust
impl Render for Workspace {
```

```rust
// Panes
 .child(
     div()
         .flex()
         .flex_col()
         .flex_1()
         .overflow_hidden()
         /*
         .child(self.center.render(
             &self.project,
             &self.follower_states,
             self.active_call(),
             &self.active_pane,
             self.zoomed.as_ref(),
             &self.app_state,
             cx,
         ))
         */
         .children(
             self.zoomed_position
                 .ne(&Some(DockPosition::Bottom))
                 .then(|| self.bottom_dock.clone()),
         ),
 )
 // Right Dock
```

#### DEFAULT_KEYMAP_PATH is located in settings/src/settings.rs

[isahc](https://github.com/sagebind/isahc) is the default HTTP client library in GPUI...

### How to have the window pop up immediately when you cargo run

```rust
cx.activate(true);
```

### How to build Zed

```rust
git submodule update --init --recursive
```

* [Noted here on how to build Zed on a mac](https://github.com/zed-industries/zed/blob/main/docs/src/developing_zed__building_zed_macos.md)
* [install postgresapp](https://postgresapp.com/downloads.html)
* [local database setup](https://zed.dev/docs/local-collaboration)


### How does open_window happen in Zed

zed/src/main.rs

* see *workspace::open_new* in *restore_or_create_workspace*
* app.on_reopen

```rust
rg picker -g Cargo.toml
rg new_view
```

### Code flow workspace

```rust
open_new
Editor::new_file
```

#### crates/zed/src/main.rs

```rust
initialize_workspace
```
