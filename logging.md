
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

### zed/src/main.rs

```rust
fn init_logger() {
        let level = LevelFilter::Info;

        // Prevent log file from becoming too large.
        const KIB: u64 = 1024;
        const MIB: u64 = 1024 * KIB;
        const MAX_LOG_BYTES: u64 = MIB;
        if std::fs::metadata(&*paths::LOG).map_or(false, |metadata| metadata.len() > MAX_LOG_BYTES)
        {
            let _ = std::fs::rename(&*paths::LOG, &*paths::OLD_LOG);
        }

        match OpenOptions::new()
            .create(true)
            .append(true)
            .open(&*paths::LOG)
        {
            Ok(log_file) => {
                let config = ConfigBuilder::new()
                    .set_time_format_str("%T")
                    .set_time_to_local(true)
                    .set_location_level(LevelFilter::Info)
                    .build();

                simplelog::WriteLogger::init(level, config, log_file)
                    .expect("could not initialize logger");
            }
            Err(err) => {
                init_stdout_logger();
                log::error!(
                    "could not open log file, defaulting to stdout logging: {}",
                    err
                );
            }
        }

}
```
