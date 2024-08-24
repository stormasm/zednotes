
### How to remove the collab crate from Zed

##### Remove the collab crate from Zed

```rust
cd crates
rm -fr collab
```

This step of removing the code is actually not necessary as simply modifying
the Cargo.toml file below is enough.

##### Modify Cargo.toml

- [Remove collab from Cargo.toml](https://github.com/stormasm/zed/commit/d2a884b20d75e64cce2c6381df81926d7ce919aa)

At this point the icons are still in the status bar...  But if you don't
mind seeing them the actual collab code itself is gone.
