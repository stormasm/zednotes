
##### discord ref on Render and RenderOnce

- [discord ref](https://discord.com/channels/869392257814519848/1199799855007158352/1201300216482119691)
- [discord ref](https://discord.com/channels/869392257814519848/1199799855007158352/1207423864448094258)
- [discord ref](https://discord.com/channels/869392257814519848/1199799855007158352/1208536615279001730)
- [discord ref](https://discord.com/channels/869392257814519848/1217227325217833043/1217283120336998502)
- [discord ref](https://discord.com/channels/869392257814519848/1199799855007158352/1261376409624907836)
- [discord ref](https://discord.com/channels/869392257814519848/1199799855007158352/1264850420937920584)
- [discord ref](https://discord.com/channels/869392257814519848/1199799855007158352/1275061349831020635)

Hey all, I'm playing with GPUI and I'm wondering about the difference between the need to impl  Render vs RenderOnce. It seems RenderOnce is nice because I can #[derive(IntoElement)] and add an the object with .child().  I haven't quite grokked the difference though. impl Render is required if I want to call AppContext::new_view.

When should I use AppContext::new_view and when should I use .child(impl RenderOnce)?
Thank you!

Zomatree — Today at 2:47 PM   
if it requires its own state you should use render and new_view

storm — Today at 2:48 PM   
And in all other cases you are saying to use RenderOnce ?
What are examples --- why would I use RenderOnce ?

Zomatree — Today at 2:49 PM   
if it doesnt need to manage its own state

storm — Today at 2:49 PM   
what is good example of that in the Zed code where RenderOnce is used because it does not manage its own state ?

Zomatree — Today at 2:50 PM   
you could do a search of the code

storm — Today at 2:51 PM   
ok thanks ! so for example checkbox and TabBar use RenderOnce --- so the state is stored somewhere else in those cases ?
in other words a lot of the crates/ui/src/components use RenderOnce

Zomatree — Today at 2:52 PM   
if they have state the parent needs to maintain it

storm — Today at 2:53 PM
thanks I will research further and think about this --- its been a question I have been having in my mind for awhile so its helpful to get your nice explanation on this topic....

Zomatree — Today at 2:54 PM
if you look at the signature RenderOnce::render takes self while Render::render takes &mut self
should be easy to figure out when you need which one

[when to use self versus mut self](https://stackoverflow.com/questions/59018413/when-to-use-self-self-mut-self-in-methods)
