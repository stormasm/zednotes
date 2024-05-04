
#### Check the following tags when going back in time

Because this is what has been pulled and is in the historical crates repos

```rust
Updating crates.io index
```

- v0.124.8 works
- v0.125.4 works
- v0.126.3 works
- v0.127.5 breaks
- v0.130.7

### More details

Go to page 6 on the releases

Broken here:
https://github.com/zed-industries/zed/commit/ced690dc0bb799e5ec2bc051700779711d1688ee

Start here:
https://github.com/zed-industries/zed/releases?page=6



- works here -> HEAD detached at e1f8a1e8b
```rust
commit e1f8a1e8b287171ea0bfd53573a64d8c3212ee28 (HEAD)
Author: Max <contact@slymax.com>
Date:   Mon Mar 11 08:56:35 2024 +0100

    Fix `<!DOCTYPE html>` syntax highlighting (#9108)
```

### Fix flickering #9012
https://github.com/zed-industries/zed/pull/9012
