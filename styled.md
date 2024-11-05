
```rust
rg gpui_macros -g Cargo.toml
```

The only place that gpui_macros is called is in the crate gpui

The only place that gpui_macros is called in gpui is in *styled.rs*

The only place that

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
