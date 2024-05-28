
### Rust Analyzer in Concert with Zed

- [this is how zed talks to rust analyzer](https://github.com/zed-industries/zed/blob/main/crates/lsp/src/lsp.rs)
- [example of rust analyzer in zed](https://github.com/zed-industries/zed/blob/main/crates/task/src/vscode_format.rs)
- [rust-analyzer.json](https://github.com/zed-industries/zed/blob/main/crates/task/test_data/rust-analyzer.json)


### Lsp Commands

- [lsp commands](https://github.com/zed-industries/zed/blob/main/crates/project/src/lsp_command.rs)

```rust
type LspRequest = lsp::request::PrepareRenameRequest;
type LspRequest = lsp::request::Rename;
type LspRequest = lsp::request::GotoDefinition;
type LspRequest = lsp::request::GotoImplementation;
type LspRequest = lsp::request::GotoTypeDefinition;
type LspRequest = lsp::request::References;
type LspRequest = lsp::request::DocumentHighlightRequest;
type LspRequest = lsp::request::HoverRequest;
type LspRequest = lsp::request::Completion;
type LspRequest = lsp::request::CodeActionRequest;
type LspRequest = lsp::request::OnTypeFormatting;
type LspRequest = lsp::InlayHintRequest;
```

### References
- [extensions](./extension.md)
- [lsp](./lsp.md)
