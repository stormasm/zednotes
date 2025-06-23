
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
