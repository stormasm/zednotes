
## How to build your own standalone gpui repo

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

### The details of how to do it

- grab a brand new fresh copy of the zed repo
- rm -fr .git [this step is not needed unless you want your own repo on github]
- copy and run this script from the top level of your new repo -> [slimcrate.sh](https://github.com/stormasm/gpuionly-250621/blob/main/slimcrate.sh)
- replace the top level *Cargo.toml* file with [this Cargo.toml file](https://github.com/stormasm/gpuionly-250621/blob/main/Cargo.toml)

### Make sure it works

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
gpui = { path = "/Users/me/gpuionly-250621/crates/gpui" }
```

Modify *crates/story/Cargo.toml* in gpui-component.

```rust
#reqwest_client = { git = "https://github.com/zed-industries/zed.git" }
#reqwest_client = { git = "https://github.com/stormasm/gpuionly-250621.git" }
reqwest_client = { path = "/Users/me/gpuionly-250621/crates/reqwest_client" }
```

#### Need to figure out the following point with the repo gpui-component

When referencing a gpui repo locally there are warnings but none when referencing
gpui remotely on github.

Even though there are warnings the applications run fine :)
