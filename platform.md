
#### gpui/src/platform

In a simple way you open the platform window and then everything from that
point on gets written to and read from the handle
of the underlying platform's window :)

see the following two methods in *window.rs*

```rust
impl Window {
    pub(crate) fn new(
        handle: AnyWindowHandle,
        options: WindowOptions,
        cx: &mut AppContext,
    ) -> Result<Self> {
```

as well as

```rust
let mut platform_window = cx.platform.open_window(
```

There are four traits in platform.rs

- pub(crate) trait Platform: 'static {
- pub(crate) trait PlatformWindow: HasWindowHandle + HasDisplayHandle {
- pub(crate) trait PlatformTextSystem: Send + Sync {
- pub(crate) trait PlatformAtlas: Send + Sync {

All of the platforms have the following files

- dispatcher.rs
- display.rs
- platform.rs
- window.rs

In linux both wayland and X11 have their own

- display.rs
- windows.rs

And the

- dispatcher.rs
- platform.rs

are the same files for both wayland and X11

#### the platform mod is referenced in the following gpui places

- app.rs
- gpui.rs
- interactive.rs
- text_system.rs
- window.rs
- app/text_context.rs
- text_system/line_layout.rs
- text_system/line_wrapper.rs
