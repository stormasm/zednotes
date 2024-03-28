### rg observe_new_views

crates/vim/src/vim.rs
85:    cx.observe_new_views(|workspace: &mut Workspace, cx| register(workspace, cx))

crates/vim/src/editor_events.rs
9:    cx.observe_new_views(|_, cx: &mut ViewContext<Editor>| {

crates/command_palette/src/command_palette.rs
31:    cx.observe_new_views(CommandPalette::register).detach();

crates/vcs_menu/src/lib.rs
21:    cx.observe_new_views(|workspace: &mut Workspace, _| {

crates/editor/src/editor.rs
245:    cx.observe_new_views(

crates/markdown_preview/src/markdown_preview.rs
12:    cx.observe_new_views(|workspace: &mut Workspace, cx| {

crates/gpui/src/app.rs
952:    pub fn observe_new_views<V: 'static>(

crates/theme_selector/src/theme_selector.rs
30:    cx.observe_new_views(

crates/auto_update/src/auto_update.rs
121:    cx.observe_new_views(|workspace: &mut Workspace, _cx| {

crates/diagnostics/src/diagnostics.rs
52:    cx.observe_new_views(ProjectDiagnosticsEditor::register)

crates/language_selector/src/language_selector.rs
22:    cx.observe_new_views(LanguageSelector::register).detach();

crates/project_panel/src/project_panel.rs
147:    cx.observe_new_views(|workspace: &mut Workspace, _| {

crates/outline/src/outline.rs
25:    cx.observe_new_views(OutlineView::register).detach();

crates/terminal_view/src/terminal_panel.rs
39:    cx.observe_new_views(

crates/terminal_view/src/terminal_view.rs
74:    cx.observe_new_views(|workspace: &mut Workspace, _| {

crates/go_to_line/src/go_to_line.rs
17:    cx.observe_new_views(GoToLine::register).detach();

crates/search/src/buffer_search.rs
57:    cx.observe_new_views(|workspace: &mut Workspace, _| BufferSearchBar::register(workspace))

crates/search/src/project_search.rs
61:    cx.observe_new_views(|workspace: &mut Workspace, _cx| {

crates/feedback/src/feedback.rs
37:    cx.observe_new_views(|workspace: &mut Workspace, cx| {

crates/tasks_ui/src/lib.rs
15:    cx.observe_new_views(

crates/welcome/src/welcome.rs
29:    cx.observe_new_views(|workspace: &mut Workspace, _cx| {

crates/welcome/src/base_keymap_picker.rs
19:    cx.observe_new_views(|workspace: &mut Workspace, _cx| {

crates/file_finder/src/file_finder.rs
38:    cx.observe_new_views(FileFinder::register).detach();

crates/collab_ui/src/chat_panel.rs
40:    cx.observe_new_views(|workspace: &mut Workspace, _| {

crates/collab_ui/src/notification_panel.rs
76:    cx.observe_new_views(|workspace: &mut Workspace, _| {

crates/collab_ui/src/collab_titlebar_item.rs
38:    cx.observe_new_views(|workspace: &mut Workspace, cx| {

  crates/tab_switcher/src/tab_switcher.rs
  39:    cx.observe_new_views(TabSwitcher::register).detach();

  crates/collab_ui/src/collab_panel.rs
  68:    cx.observe_new_views(|workspace: &mut Workspace, _| {

  crates/extensions_ui/src/extensions_ui.rs
  30:    cx.observe_new_views(move |workspace: &mut Workspace, cx| {

  crates/project_symbols/src/project_symbols.rs
  21:    cx.observe_new_views(

  crates/recent_projects/src/recent_projects.rs
  32:    cx.observe_new_views(RecentProjects::register).detach();

  crates/language_tools/src/syntax_tree_view.rs
  21:    cx.observe_new_views(|workspace: &mut Workspace, _| {

  crates/language_tools/src/lsp_log.rs
  84:    cx.observe_new_views(move |workspace: &mut Workspace, cx| {

  crates/zed/src/main.rs
  1081:        cx.observe_new_views(move |editor: &mut Editor, cx: &mut ViewContext<Editor>| {

  crates/zed/src/zed.rs
  111:    cx.observe_new_views(move |workspace: &mut Workspace, cx| {

  crates/journal/src/journal.rs
  65:    cx.observe_new_views(

  crates/assistant/src/assistant_panel.rs
  54:    cx.observe_new_views(
  
