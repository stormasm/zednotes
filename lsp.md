
The way Zed finds the language server for a particular language is via the *language_server_command*
in the
[extension_api](https://github.com/zed-industries/zed/blob/main/crates/extension_api/src/extension_api.rs).

- [Lsp Language Servers written in Rust](https://microsoft.github.io/language-server-protocol/implementors/servers/)
- erlang
- gleam
- lox
- pest

- [Tree Sitter Grammar DSL](https://tree-sitter.github.io/tree-sitter/creating-parsers#the-grammar-dsl)

#### This is the code that talks to rust analyzer

- Rust analyzer gets fired up
- Rust analyzer gets communicated with

```rust
/// A running language server process.
pub struct LanguageServer

impl LanguageServer
```

### References
- [rust-analyzer](./rustanalyzer.md)
