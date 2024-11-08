
#### gpui/src/platform

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

are the same files for both

#### platform is referenced in the following gpui places

- app.rs
- gpui.rs
- interactive.rs
- text_system.rs
- window.rs
- app/text_context.rs
- text_system/line_layout.rs
- text_system/line_wrapper.rs
