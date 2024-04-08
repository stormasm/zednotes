
- [simplelog api](https://docs.rs/simplelog/0.12.2/simplelog/)
- [simplelog](https://github.com/drakulix/simplelog.rs)

### How Logging works in Zed

zed/src/main.rs

```rust
init_logger();

log::info!("========== starting zed ==========");
```

### Location of logfiles

zed: open logs

/Users/ma/Library/Logs/Zed   
Location of db file:   
/Users/ma/Library/Application Support/Zed/db/0-dev   
Which is a sqlite database.

In main.rs see *init_paths* which points to LOGS_DIR   
which is located in crates/util/src/paths.rs


### Detailed examples

copilot_completion_provider.rs

```rust
fn discard(&mut self, cx: &mut ModelContext<Self>) {
    let settings = AllLanguageSettings::get_global(cx);
    if !settings.copilot.feature_enabled {
        return;
    }

    self.copilot
        .update(cx, |copilot, cx| {
            copilot.discard_completions(&self.completions, cx)
        })
        .detach_and_log_err(cx);
    if let Some(telemetry) = self.telemetry.as_ref() {
        telemetry.report_copilot_event(None, false, self.file_extension.clone());
    }
}
```
