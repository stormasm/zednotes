
In Zed there are several places in the code base where elements are defined and implemented.

Besides the obvious places like the *gpui* and *ui* crates the following places exist.

You can find these spots in the code base by rip-greping for *prepaint*

- editor/src/element.rs
- markdown/src/markdown.rs
- terminal_view/src/terminal_element.rs
- workspace/src/pane_group.rs

### Legacy Notes

##### March 17, 2024

##### Tpisto Question

Thank you for @Nowlow for good question. I'm trying to figure out exactly the same that what is the way to make stateful component. By looking the Zed repo I see that they are not using models for state, but there is that "Stateful" struct that wraps the stateful component. @mikayla I see that you have done the Stateful struct, please could you explain how it works? I have tried to understand it, but it seems just to be wrapper that just puts the element into Stateful { element: YourElement }... My goal is to create following simple component as stateful example. So that the border green state (on_mouse_down) is handled by the component itself. The value (true/false) is easy, because the parent will pass it down.

So, the goals:

- Stateful component should be Element that it can be used like .child(checkbox().id(1).on_click(...
- I would like to understand how to make stateful component without Model and action subscribers to hold "mouse_is_down" value for my component.
- I would like to understand how the Stateful construct works in GPUI for your elements.
- Extra: Would be absolutely wonderful and would make my day if someone could nicely explain the Element trait "before_layout", "after_layout" and "paint" concepts.

##### Mikayla Answer

The stateful component portion of Zed is incomplete. It's supposed to fill exactly the role you're looking for, but it currently doesn't actually have a way of storing it's only while visible state internally, or exposing it externally. Your best option is to store all of the state on the parent, either wrapped in a RefLock or a GPUI Model, and then hand it into your element. This is how the List and Uniform list elements work today.

In GPUI, painting your scene involves three traversals of the whole DAG:

- before_layout, this is where your element tells our layout engine (Taffy) how it wants to be positioned in relation to the elements around it
- after_layout, once Taffy has collected all of this data, it runs it's algorithms and tells us where we all are. At this phase we resolve hit detection, giving elements a chance to determine if the mouse intersects their new position (e.g. for determining if hover styles need to be applied for this frame)
- paint, once all of this data has been gathered, it's time to actually render this Element to the screen. In this phase, you should have all of the information you need to call the  ElementContext::paint_* methods to render everything.

Note that Elements are ephemeral, they only last as long as the View containing them is unchanged. As soon as a new frame detects that their view has been changed, they are tossed out and recomputed. If you want stuff to stick around, you need to tag it with an ElementID and store it in GPUI, where it will only be held as long as the tree still holds that ElementID in that location, or you need to put it in a View.
Also, if you want to see an existing checkbox implementation in GPUI, you can look at crates/ui/src/components/checkbox

- [ref](https://discord.com/channels/869392257814519848/1199799855007158352/1218957719189586040)
