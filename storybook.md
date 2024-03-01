
### Cargo.toml

```rust
+#theme.workspace = true
+theme = { workspace = true, features = ["stories"] }
```

### src/story_selector.rs

```rust
+use theme::{ColorsStory, PlayerStory};

ViewportUnits,
ZIndex,
Picker,
+   Colors,
+   Player,

Self::ZIndex => cx.new_view(|_| ZIndexStory).into(),
Self::Picker => PickerStory::new(cx).into(),
+   Self::Colors => cx.new_view(|_| ColorsStory).into(),
+   Self::Player => cx.new_view(|_| PlayerStory).into(),
```
