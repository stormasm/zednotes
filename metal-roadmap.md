
I asked a question about this subject on [discord](https://discord.com/channels/869392257814519848/1199799855007158352/1414011431833309225) but got no response
so I thought it made more sense to file it as an issue to keep track
of whats going to happen moving forward.

gpui uses the [metal crate](https://github.com/gfx-rs/metal-rs) which is deprecated.

There is a `TODO` note in [gpui Cargo.toml](https://github.com/zed-industries/zed/blob/main/crates/gpui/Cargo.toml) to replace the metal crate with objc2

```rust
objc2 = { version = "0.6", optional = true }
objc2-metal = { version = "0.3", optional = true }
#TODO: replace with "objc2"
metal.workspace = true
```

Blade currently uses objc2 and objc2-metal in the [Blade Renderer](https://github.com/zed-industries/zed/blob/main/crates/gpui/src/platform/blade/blade_renderer.rs)

Is this on the Roadmap to happen prior to publishing out gpui to crates.io ?
