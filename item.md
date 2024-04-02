
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
