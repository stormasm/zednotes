

##### fe59d983eb1e12321d92daea3aa92e22e4cf5aa2

```rust
Updating fc152eb459..fe59d983eb
Fast-forward
 crates/gpui3/examples/animation.rs             |   68 +-
 crates/gpui3/examples/gif_viewer.rs            |   28 +-
 crates/gpui3/examples/hello_world.rs           |   40 +-
 crates/gpui3/examples/image/image.rs           |   25 +-
 crates/gpui3/examples/image_loading.rs         |  175 +--
 crates/gpui3/examples/input.rs                 | 1408 ++++++++++++------------
 crates/gpui3/examples/opacity.rs               |   16 +-
 crates/gpui3/examples/painting.rs              |   42 +-
 crates/gpui3/examples/set_menus.rs             |   30 +-
 crates/gpui3/examples/shadow.rs                |   28 +-
 crates/gpui3/examples/svg/svg.rs               |   64 +-
 crates/gpui3/examples/text_wrapper.rs          |  148 +--
 crates/gpui3/examples/uniform_list.rs          |   33 +-
 crates/gpui3/examples/window.rs                |  197 ++--
 crates/gpui3/examples/window_positioning.rs    |  101 +-
 crates/gpui3/examples/window_shadow.rs         |  321 +++---
 crates/gpui3/notes.md                          |    7 +-
 crates/gpui3/src/app.rs                        |   76 +-
 crates/gpui3/src/app/async_context.rs          |  171 +--
 crates/gpui3/src/app/model_context.rs          |   26 +
 crates/gpui3/src/app/test_context.rs           |  183 ++--
 crates/gpui3/src/element.rs                    |   83 +-
 crates/gpui3/src/elements/div.rs               |   70 +-
 crates/gpui3/src/elements/img.rs               |   38 +-
 crates/gpui3/src/elements/svg.rs               |    4 +-
 crates/gpui3/src/elements/text.rs              |    2 +-
 crates/gpui3/src/elements/uniform_list.rs      | 1044 +++++++++---------
 crates/gpui3/src/gpui.rs                       |    1 +
 crates/gpui3/src/input.rs                      |  387 ++++---
 crates/gpui3/src/interactive.rs                |  113 +-
 crates/gpui3/src/platform.rs                   |   88 +-
 crates/gpui3/src/platform/test/window.rs       |    4 +-
 crates/gpui3/src/platform/windows/clipboard.rs |    2 +-
 crates/gpui3/src/window.rs                     | 5888 +++++++++++++++++++-------------------------------------------------------------------------------
 crates/gpui3/src/window/prompts.rs             |  338 +++---
 35 files changed, 3872 insertions(+), 7377 deletions(-)
 ```
