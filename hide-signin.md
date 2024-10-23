
#### crates/title_bar/src/title_bar.rs

```rust
//For settings related to the Title Bar (like hiding Sign in button)
use anyhow::Result;
use settings::{Settings, SettingsSources};
```

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

Add *TitleBarSettings::register(cx);* to the init method along with this struct

```rust
//Title bar settings
pub struct TitleBarSettings(pub bool);
```

Inside *impl Render for TitleBar {*

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
