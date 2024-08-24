
## Step One: Remove the collab crate from Zed

```rust
cd crates
rm -fr collab
```

This step of removing the code is actually not necessary as simply modifying
the Cargo.toml file below is enough.

##### Modify Cargo.toml

- [Remove collab from Cargo.toml](https://github.com/stormasm/zed/commit/d2a884b20d75e64cce2c6381df81926d7ce919aa)

At this point the icons are still in the status bar...  But if you don't
mind seeing them the actual collab code itself is gone and everything works

## Step Two: Removing the collab_ui crate

```rust
cd crates
rm -fr collab_ui
```

Now the icons are no longer in the status bar...

Again you don't actually have to remove the code if you don't want to.  

Zed works fine with the *collab_ui* code in there but none of the functionality of
the collab code is present.

### A minor bug still exists

where the branch name is overwritten by the stop lights on a mac...

Help is appreciated in fixing this minor detail...
