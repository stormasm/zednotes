



### Google

In React, a dispatch tree is a data structure that represents the flow of actions through a Redux application. It is a tree of objects, where each object represents a reducer. Reducers are functions that take the current state of the application and an action, and return the next state.

The dispatch tree is used by the Redux store to determine which reducers should be called when an action is dispatched. The store starts at the root of the tree and calls each reducer in turn, passing in the current state and the action. The reducers then update the state accordingly.

The dispatch tree is a powerful tool that can be used to manage the state of complex React applications. It allows you to isolate different parts of your application's state and to ensure that they are updated in a consistent way.

Here is an example of a dispatch tree:

```json
{
  root: {
    reducer: rootReducer,
    children: {
      users: {
        reducer: usersReducer,
        children: {}
      },
      products: {
        reducer: productsReducer,
        children: {}
      }
    }
  }
}
```

In this example, the dispatch tree has two children: users and products. Each child represents a reducer that is responsible for managing a different part of the application's state.

When an action is dispatched, the Redux store starts at the root of the tree and calls each reducer in turn, passing in the current state and the action. The reducers then update the state accordingly.

For example, if the action is ADD_USER, the store will call the usersReducer reducer. The usersReducer reducer will then update the state to add the new user.

The dispatch tree is a powerful tool that can be used to manage the state of complex React applications. It allows you to isolate different parts of your application's state and to ensure that they are updated in a consistent way.

- what is a dispatch tree in react ?
- [google link](https://www.google.com/search?q=what+is+a+dispatch+tree+in+react&sca_esv=4d50ecf86976fd48&rlz=1C5CHFA_enUS1045US1045&sxsrf=ADLYWIIoU0kdc9UscG1f60VY6xnwQwqlTA%3A1715102445713&ei=7WI6ZtKSK4eB0PEPy8eNmAk&ved=0ahUKEwiSvZ7AhvyFAxWHADQIHctjA5MQ4dUDCBA&uact=5&oq=what+is+a+dispatch+tree+in+react&gs_lp=Egxnd3Mtd2l6LXNlcnAiIHdoYXQgaXMgYSBkaXNwYXRjaCB0cmVlIGluIHJlYWN0MgUQIRigATIFECEYoAEyBRAhGKABMgUQIRigATIFECEYoAEyBRAhGJ8FSJEpUNIHWJ4gcAF4AZABAJgBnAGgAdYLqgEDOS42uAEDyAEA-AEBmAIKoAK4B8ICChAAGLADGNYEGEfCAgQQIRgVmAMAiAYBkAYIkgcDNi40oAedWQ&sclient=gws-wiz-serp)


### Old Code

```rust
#[derive(Clone, Copy, Debug, Eq, PartialEq, Hash)]
pub(crate) struct DispatchNodeId(usize);

pub(crate) struct DispatchTree {
    node_stack: Vec<DispatchNodeId>,
    pub(crate) context_stack: Vec<KeyContext>,
    nodes: Vec<DispatchNode>,
    focusable_node_ids: FxHashMap<FocusId, DispatchNodeId>,
    view_node_ids: FxHashMap<EntityId, DispatchNodeId>,
    keystroke_matchers: FxHashMap<SmallVec<[KeyContext; 4]>, KeystrokeMatcher>,
    keymap: Rc<RefCell<Keymap>>,
    action_registry: Rc<ActionRegistry>,
}

#[derive(Default)]
pub(crate) struct DispatchNode {
    pub key_listeners: Vec<KeyListener>,
    pub action_listeners: Vec<DispatchActionListener>,
    pub context: Option<KeyContext>,
    focus_id: Option<FocusId>,
    view_id: Option<EntityId>,
    parent: Option<DispatchNodeId>,
}

type KeyListener = Rc<dyn Fn(&dyn Any, DispatchPhase, &mut ElementContext)>;

#[derive(Clone)]
pub(crate) struct DispatchActionListener {
    pub(crate) action_type: TypeId,
    pub(crate) listener: Rc<dyn Fn(&dyn Any, DispatchPhase, &mut WindowContext)>,
}
```

### Latest Code

```rust
#[derive(Clone, Copy, Debug, Eq, PartialEq, Hash)]
pub(crate) struct DispatchNodeId(usize);

pub(crate) struct DispatchTree {
    node_stack: Vec<DispatchNodeId>,
    pub(crate) context_stack: Vec<KeyContext>,
    view_stack: Vec<EntityId>,
    nodes: Vec<DispatchNode>,
    focusable_node_ids: FxHashMap<FocusId, DispatchNodeId>,
    view_node_ids: FxHashMap<EntityId, DispatchNodeId>,
    keystroke_matchers: FxHashMap<SmallVec<[KeyContext; 4]>, KeystrokeMatcher>,
    keymap: Rc<RefCell<Keymap>>,
    action_registry: Rc<ActionRegistry>,
}

#[derive(Default)]
pub(crate) struct DispatchNode {
    pub key_listeners: Vec<KeyListener>,
    pub action_listeners: Vec<DispatchActionListener>,
    pub modifiers_changed_listeners: Vec<ModifiersChangedListener>,
    pub context: Option<KeyContext>,
    pub focus_id: Option<FocusId>,
    view_id: Option<EntityId>,
    parent: Option<DispatchNodeId>,
}

type KeyListener = Rc<dyn Fn(&dyn Any, DispatchPhase, &mut WindowContext)>;
type ModifiersChangedListener = Rc<dyn Fn(&ModifiersChangedEvent, &mut WindowContext)>;

#[derive(Clone)]
pub(crate) struct DispatchActionListener {
    pub(crate) action_type: TypeId,
    pub(crate) listener: Rc<dyn Fn(&dyn Any, DispatchPhase, &mut WindowContext)>,
}

```
