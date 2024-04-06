

```rust
rg right_click_menu
```

Right click menus are used in
- workspace/src/dock.rs
- workspace/src/pane.rs


### Kallax

The reason I got turned on to this idea is because an old version of Kallax
used overlays which are now called [anchored](https://github.com/zed-industries/zed/blob/main/crates/gpui/src/elements/anchored.rs).

Anchored is used in Kallax as a dropdown to both *play* and *queue* a track.

```rust
gco 4dc61f7ccd6ac77a6f03d90d7ee80e855b0f32b9
```

https://github.com/zed-industries/zed/tree/4dc61f7ccd6ac77a6f03d90d7ee80e855b0f32b9

### gpui: Rework overlay element #9911
https://github.com/zed-industries/zed/pull/9911

- [right_click_menu.rs history](https://github.com/zed-industries/zed/commits/main/crates/ui/src/components/right_click_menu.rs)
