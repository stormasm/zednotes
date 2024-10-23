
## How to Hide Sign-In in Zed

- Thanks to [evanheller](https://github.com/evanheller)
- [Zed Issue 12325](https://github.com/zed-industries/zed/issues/12325#issuecomment-2432769188)
- [Zed PR 19581](https://github.com/zed-industries/zed/pull/19581)

More documentation and code for this on my personal branch

- [stormasm hide_signin branch](https://github.com/stormasm/zed/tree/hide_signin)

## Along with step by step code instructions

#### modify default.json

In the file

- [assets/settings/default.json](https://github.com/zed-industries/zed/blob/main/assets/settings/default.json)

add this line

```rust
"titlebar_signin": false,
```

which sits in the larger context of

```rust
"toolbar": {
  // Whether to display the terminal title in its toolbar.
  "title": true
}
// Set the terminal's font size. If this option is not included,
// the terminal will default to matching the buffer's font size.
// "font_size": 15,
// Set the terminal's font family. If this option is not included,
// the terminal will default to matching the buffer's font family.
// "font_family": "Zed Plex Mono",
// Set the terminal's font fallbacks. If this option is not included,
// the terminal will default to matching the buffer's font fallbacks.
// This will be merged with the platform's default font fallbacks
// "font_fallbacks": ["FiraCode Nerd Fonts"],
// Sets the maximum number of lines in the terminal's scrollback buffer.
// Default: 10_000, maximum: 100_000 (all bigger values set will be treated as 100_000), 0 disables the scrolling.
// Existing terminals will not pick up this change until they are recreated.
// "max_scroll_history_lines": 10000,
},
"titlebar_signin": false,
"code_actions_on_format": {},
/// Settings related to running tasks.
"tasks": {
"variables": {}
},
```

Modify Cargo.toml with one extra dependency

##### crates/title_bar/Cargo.toml

```rust
[dependencies]
anyhow.workspace = true
```

And modify the file *title_bar.rs* with the following changes

##### crates/title_bar/src/title_bar.rs

```rust
//For settings related to the Title Bar (like hiding Sign in button)
use anyhow::Result;
use settings::{Settings, SettingsSources};
```

## Next item
---

```rust
pub fn init(cx: &mut AppContext) {
    TitleBarSettings::register(cx);
    cx.observe_new_views(|workspace: &mut Workspace, cx| {
        let item = cx.new_view(|cx| TitleBar::new("title-bar", workspace, cx));
        workspace.set_titlebar_item(item.into(), cx)
    })
    .detach();
}
```

Add the following line of code to the above *init* method along with this struct

```rust
TitleBarSettings::register(cx);
```

## Next item
---

Just above

```rust
impl Render for TitleBar {
    fn render(&mut self, cx: &mut ViewContext<Self>) -> impl IntoElement {
```

add this struct

```rust
//Title bar settings
pub struct TitleBarSettings(pub bool);
```

## Next item
---

Inside

```rust
impl Render for TitleBar {
```

Add this line of code

```rust
//For hiding Sign in
let show_signin = TitleBarSettings::get_global(cx).0;
```

along with this modification

```rust
} else {
    if show_signin {
        el.children(self.render_connection_status(status, cx))
            .child(self.render_sign_in_button(cx))
            .child(self.render_user_menu_button(cx))
    } else {
        el.children(self.render_connection_status(status, cx))
            .child(self.render_user_menu_button(cx))
    }
}
```

## Next item
---

Add this code to the end of the file

```rust
impl Settings for TitleBarSettings {
    const KEY: Option<&'static str> = Some("titlebar_signin");

    type FileContent = Option<bool>;

    fn load(sources: SettingsSources<Self::FileContent>, _: &mut AppContext) -> Result<Self> {
        Ok(Self(
            sources
                .user
                .or(sources.server)
                .copied()
                .flatten()
                .unwrap_or(sources.default.ok_or_else(Self::missing_default)?),
        ))
    }
}
```

remove references to the method *render_ssh_project_host*

```rust
if self.project.read(cx).is_via_ssh() {
    return self.render_ssh_project_host(cx);
}
```

or add truncate here in *render_ssh_project_host*

```rust
div()
    .max_w_32()
    .overflow_hidden()
    .truncate()
    .text_ellipsis()
    .child(Label::new(nickname.clone()).size(LabelSize::Small)),
```
