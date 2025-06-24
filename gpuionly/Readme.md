

- zed/crates/gpui/build.rs
- macos-blade

If you compile gpui-component you will see it pull in

- blade-graphics
- blade-macros
- blade-util

If you look at Cargo.lock in gpui-component you will see why

Also the source shows this -

```rust
[[package]]
name = "gpui"
version = "0.1.0"
source = "git+https://github.com/zed-industries/zed.git#a067c16c823354da63966273ac15d1aa93c0e922"
dependencies = [
 "anyhow",
 "as-raw-xcb-connection",
 "ashpd",
 "async-task",
 "bindgen 0.71.1",
 "blade-graphics",
 "blade-macros",
 "blade-util",
```

Note how it is depending on zed.git which in my particular case is not true.

So does your Cargo.lock file pull in the blade stuff ?     
It does but it is not showing the source

---

The following crates are needed along with gpui

- collections
- gpui
- gpui-macros
- http_client
- media
- refineable
- semantic_version
- sum_tree
- util

### Dependency crates for gpuionly

```rust
members = [
    "crates/collections",
    "crates/gpui",
    "crates/gpui_macros",
    "crates/http_client",
    "crates/media",
    "crates/refineable",
    "crates/semantic_version",
    "crates/sum_tree",
    "crates/util",
]
```

If you remove the image examples then you no longer need the following dependencies:

- reqwest_client

---

- The crate *sum_tree* needs the crate *zlog* for testing

---

- The crate *reqwest_client* depends on http_client & http_client_tls
