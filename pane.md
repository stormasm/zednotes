
So there are several different concepts going on with pane that are kind
of subtle.

The Render method of Pane has the following topics:

- render_tab_bar
- toolbar
- item

```rust
if let Some(item) = self.active_item() {
    div.v_flex()
        .child(self.toolbar.clone())
        .child(item.to_any())
 ```

- The tab_bar is at the top of the screen and has all of the items or tabs
 or editors.
- The toolbar has the search_bar along with the quick_action_bar
- And then there is the active_item

The pane_group holds everything in place and deals with splitting the items.
