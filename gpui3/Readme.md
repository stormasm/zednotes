
#### Response to my question

- [mikayla discord response](https://discord.com/channels/869392257814519848/1199799855007158352/1325367057671258129)

Probably because the ideas are unnecessary   
initially view pointers carried the window a view was being rendered in   
But that got removed as we updated to a rewrite of GPUI   
so Views have kind of been in this strange vestigial area   
for a while where they’re the exact same as Models….   
but all of their methods provide you with a ViewContext so they need a new type   
but without a ViewContext, that type isn’t needed, meaning we can simplify everything 🙂

#### My question

storm — Jan 4, 2025 gpui forum on Zed at 9:47 PM
https://github.com/zed-industries/zed/pull/22632

I guess there have been some different attempts at these concepts...

Along with

https://github.com/zed-industries/zed/tree/gpui3-take2

and
https://github.com/zed-industries/zed/tree/gpui3.1

etc....

What have been the lessons learned as the experiment continues...

I kind of find this process fascinating in the respect that Nathan and others are really looking for the correct way forward.

Very cool that this is being done 🙂
What are the main motivating factors and limitations of the current gpui API and what are the goals of the future API ?
Eliminate GPUI View, ViewContext, and WindowContext types
storm — Yesterday at 9:54 PM
Why is the elimination of GPUI View a goal here ?

What will replace the GPUI View and why will the API be "better" without it ?
The following branch was the first attempt ---- and I guess you all learned something from it that did not work out ?

Curious to know what that was....

https://github.com/zed-industries/zed/tree/gpui3








- working off this [branch](https://github.com/zed-industries/zed/compare/main...gpui3)

##### window.rs

- remove `pub struct ViewContext`
- remove `pub struct WindowContext`

and completely remove the file `view.rs`

---

#### When does the file "view.rs" get removed from the code ?

On Nov 24 `view.rs` is removed here with the comment `WIP`   
It is the first `WIP` after `Checkpoint`
```rust   
e28104b2e8b2f7649137dd81411435d02d577be4
```
