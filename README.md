
### How to build Zed

```rust
git submodule update --init --recursive
```

* [Noted here on how to build Zed on a mac](https://github.com/zed-industries/zed/blob/main/docs/src/developing_zed__building_zed_macos.md)
* [install postgresapp](https://postgresapp.com/downloads.html)
* [local database setup](https://zed.dev/docs/local-collaboration)


### How does open_window happen in Zed

zed/src/main.rs

* see *workspace::open_new* in *restore_or_create_workspace*
* app.on_reopen

### Location of logfiles

/Users/ma/Library/Logs/Zed   
Location of db file:   
/Users/ma/Library/Application Support/Zed/db/0-dev   
Which is a sqlite database.

In main.rs see *init_paths* which points to LOGS_DIR   
which is located in crates/util/src/paths.rs

```rust
rg picker -g Cargo.toml
rg new_view
```

### Code flow workspace

```rust
open_new
Editor::new_file
```

#### crates/zed/src/main.rs

```rust
initialize_workspace
```
