
```rust
rg gpui_macros -g Cargo.toml
```

The only place that gpui_macros is called is in the crate gpui

The only place that gpui_macros is called in gpui is in *styled.rs*

The only place where the Styled trait is used is below.

```rust
rg "impl Styled"
```

```rust
src/style.rs
249:impl Styled for StyleRefinement {

src/elements/svg.rs
105:impl Styled for Svg {

src/elements/list.rs
863:impl Styled for List {

src/elements/uniform_list.rs
133:impl Styled for UniformList {

src/elements/img.rs
275:impl Styled for Img {

src/elements/div.rs
1109:impl Styled for Div {

src/elements/surface.rs
106:impl Styled for Surface {

src/elements/text.rs
136:impl StyledText {
```

---

```rust
rg taffy
```

Where taffy is referenced in gpui.

```rust
crates/gpui/src/gpui.rs
94:mod taffy;
147:pub use taffy::{AvailableSpace, LayoutId};
156:use taffy::TaffyLayoutEngine;

crates/gpui/src/style.rs
16:pub use taffy::style::{

crates/gpui/src/styled.rs
12:use taffy::style::{AlignContent, Display};

crates/gpui/src/element.rs
3://! standards as implemented by [taffy](https://github.com/DioxusLabs/taffy). Most of the time,

crates/gpui/src/elements/div.rs
40:use taffy::style::Overflow;

crates/gpui/src/elements/uniform_list.rs
2://! Rather than use the full taffy layout system, uniform_list simply measures
15:use taffy::style::Overflow;

crates/gpui/Cargo.toml
106:taffy = "0.4.3"

crates/gpui/src/elements/anchored.rs
2:use taffy::style::{Display, Position};

crates/gpui/src/elements/list.rs
19:use taffy::style::Overflow;
```

#### References

- [Gpui: The Big Picture](https://github.com/zed-industries/zed/tree/main/crates/gpui#the-big-picture)
