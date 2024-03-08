
##### March 07, 2024

mikayla —  
Yeah, cx.background_executor().spawn(async { 0u8 }) will you give you back a Task<u8>, that you can await to get that 0!

Matthias —   
That makes so much sense 🤦‍♂️ luckily I haven’t had to work across threads a lot so far

[ref](https://discord.com/channels/869392257814519848/1199799855007158352/1215407613206986823)

##### March 05, 2024

Hi, is it possible to store state on a RenderOnce  "component" or how would be the idiomatic way to handle, for example, a toggleable button with internal state?

maxdeviant — Today at 12:10 PM

The state would need to be stored on a view and passed in. We don’t support components having their own state, currently

[ref](https://discord.com/channels/869392257814519848/1199799855007158352/1214662036257112105)

Continue to take a look further at the continuuing discussion on this topic following this link.
