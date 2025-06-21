
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
