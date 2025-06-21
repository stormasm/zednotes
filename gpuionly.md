
## How to Build your own standalone gpui crate

If you see any issues with these instructions let me know and I will
modify them.

##### The following 13 crates are needed to build gpui standalone

- collections
- gpui
- gpui_macros
- http_client
- http_client_tls
- media
- refineable
- reqwest_client
- semantic_version
- sum_tree
- util
- util_macros
- zlog

##### How to build your own gpui standalone crate

- grab a brand new fresh copy of the zed repo
- copy and run this script -> [slimcrate.sh](https://github.com/stormasm/gpuionly-250621/blob/main/slimcrate.sh)
- replace the top level *Cargo.toml* file with [this Cargo.toml file](https://github.com/stormasm/gpuionly-250621/blob/main/Cargo.toml)

##### Make sure it works

Run a couple of the gpui examples

```rust
cargo run --example hello_world
cargo run --example image_gallery
```

### How to use it with other gpui repos

I will use [gpui-component](https://github.com/longbridge/gpui-component) as a working example.

Modify the top level *Cargo.toml* file in gpui-component

```rust
#gpui = { git = "https://github.com/zed-industries/zed.git" }
gpui = { git = "https://github.com/stormasm/gpuionly-250621.git" }
```

Modify *crates/story/Cargo.toml* in gpui-component.

```rust
#reqwest_client = { git = "https://github.com/zed-industries/zed.git" }
reqwest_client = { git = "https://github.com/stormasm/gpuionly-250621.git" }
```

### How to reference gpuionly from your local disk instead of Github

Modify the top level *Cargo.toml* file in gpui-component

```rust
#gpui = { git = "https://github.com/zed-industries/zed.git" }
#gpui = { git = "https://github.com/stormasm/gpuionly-250621.git" }
gpui = { path = "/User/me/gpuionly-250621/crates/gpui" }
```

Modify *crates/story/Cargo.toml* in gpui-component.

```rust
#reqwest_client = { git = "https://github.com/zed-industries/zed.git" }
#reqwest_client = { git = "https://github.com/stormasm/gpuionly-250621.git" }
reqwest_client = { path = "/Users/me/gpuionly-250621/crates/reqwest_client" }
```
