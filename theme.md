
### Theme key files

[theme/src/schema.rs](https://github.com/zed-industries/zed/blob/998f6cf80d3de4c289869edfa20e847605465776/crates/theme/src/schema.rs)

[schema/themes/v0.1.0.json](https://zed.dev/schema/themes/v0.1.0.json)

rg theme::init

see the assets folder at the top level for more details.

### Theme examples

rg match_background

### Theme PRs

* [Watch the themes directory for changes #7173](https://github.com/zed-industries/zed/pull/7173)
* [7154](https://github.com/zed-industries/zed/pull/7154)
* [7129](https://github.com/zed-industries/zed/pull/7154)
* [Show an example of a Theme 7027](https://github.com/zed-industries/zed/pull/7027)
* [7025](https://github.com/zed-industries/zed/pull/7025)
* [7023](https://github.com/zed-industries/zed/pull/7023)
* [Auto switching light/dark theme according to system settings #6881](https://github.com/zed-industries/zed/pull/6881)
* [Add experimental.theme_overrides to settings file #6791](https://github.com/zed-industries/zed/pull/6791)

### Theme example -> settings.json

```rust
{
  "language_overrides": {
    "Rust": {
      "enable_language_server": true
    }
  },
  "experimental.theme_overrides": {
    "editor.background": "#000000"
  }
}
```
