
### Pane

```rust
/// A container for 0 to many items that are open in the workspace.
/// Treats all items uniformly via the [`ItemHandle`] trait, whether it's an editor, search results multibuffer, terminal or something else,
/// responsible for managing item tabs, focus and zoom states and drag and drop features.
/// Can be split, see `PaneGroup` for more details.
pub struct Pane {
```

### rg "impl Item for"

This shows which *Items* are similar to the WelcomePage

- debug: open syntax tree view   
- debug: open language server logs - LspLogView
- zed: extensions   
- diagnostics: deploy   
- project search:   

- image_viewer  
- markdown_preview

These items will show up as views in Zed similar to the WelcomePage

Note that this is different than a regular view in a gpui application
as this view can sit inside a workspace in Zed and in the future
any gpui application that uses the *workspace* concept.

Eventually in order to get to this place I would like to remove the workspace
dependency on *Project* which is not needed for most applications that are
not part of Zed.
