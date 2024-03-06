
Hi, is it possible to store state on a RenderOnce  "component" or how would be the idiomatic way to handle, for example, a toggleable button with internal state?

maxdeviant — Today at 12:10 PM

The state would need to be stored on a view and passed in. We don’t support components having their own state, currently

[discord ref](https://discord.com/channels/869392257814519848/1199799855007158352/1214662036257112105)
