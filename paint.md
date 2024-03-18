The stateful component portion of Zed is incomplete. It's supposed to fill exactly the role you're looking for, but it currently doesn't actually have a way of storing it's only while visible state internally, or exposing it externally. Your best option is to store all of the state on the parent, either wrapped in a RefLock or a GPUI Model, and then hand it into your element. This is how the List and Uniform list elements work today.

In GPUI, painting your scene involves three traversals of the whole DAG:

- before_layout, this is where your element tells our layout engine (Taffy) how it wants to be positioned in relation to the elements around it
- after_layout, once Taffy has collected all of this data, it runs it's algorithms and tells us where we all are. At this phase we resolve hit detection, giving elements a chance to determine if the mouse intersects their new position (e.g. for determining if hover styles need to be applied for this frame)
- paint, once all of this data has been gathered, it's time to actually render this Element to the screen. In this phase, you should have all of the information you need to call the  ElementContext::paint_* methods to render everything.

Note that Elements are ephemeral, they only last as long as the View containing them is unchanged. As soon as a new frame detects that their view has been changed, they are tossed out and recomputed. If you want stuff to stick around, you need to tag it with an ElementID and store it in GPUI, where it will only be held as long as the tree still holds that ElementID in that location, or you need to put it in a View.
Also, if you want to see an existing checkbox implementation in GPUI, you can look at crates/ui/src/components/checkbox

- [ref](https://discord.com/channels/869392257814519848/1199799855007158352/1218957719189586040)
