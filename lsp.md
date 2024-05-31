
- languages is for any language-related settings.
- lsp is for passing specific options to a language server (which could be used for multiple languages)

[discord](https://discord.com/channels/869392257814519848/873293828805771284/1245827506532257862)

- [Blog post by Max: Language Support in Zed Part One](https://zed.dev/blog/language-extensions-part-1)

The way Zed finds the language server for a particular language is via the *language_server_command*
in the
[extension_api](https://github.com/zed-industries/zed/blob/main/crates/extension_api/src/extension_api.rs).

```rust
/// Returns the command used to start the language server for the specified language.
fn language_server_command(
    &mut self,
    language_server_id: &LanguageServerId,
    worktree: &Worktree,
) -> Result<Command>;
```

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
- [extensions](./extension.md)
- [rust-analyzer](./rustanalyzer.md)
