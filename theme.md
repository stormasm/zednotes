
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
