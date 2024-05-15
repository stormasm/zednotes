
The Zed crate [tasks_ui](https://github.com/zed-industries/zed/tree/main/crates/tasks_ui) runs inside the integrated Zed terminal. Its mainly a way to run tests in the Zed editor when you are inside a particular crate.

This is cool !  I didn't realize this before and it adds some additional nice functionality to running the tests inside Zed or any other development package you are editing...

The motivation for this concept comes from [Vscode](https://code.visualstudio.com/docs/editor/tasks)

```rust
rg Task\<Result
```

For a great example of how Tasks work inside the Zed source code check out the function
[parse_markdown_in_background](https://github.com/zed-industries/zed/blob/main/crates/markdown_preview/src/markdown_preview_view.rs#L338)

see [executor](./executor.md) for more details...

### References

Zed modeled their task system based on Microsoft's Vscode:
- [Integrate with External Tools via Tasks](https://code.visualstudio.com/docs/editor/tasks)
