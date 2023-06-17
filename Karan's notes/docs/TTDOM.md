The virtual DOM was created to address performance issues caused by frequent manipulation of the real DOM. It is a lightweight, in-memory representation of the real DOM, which can be later used as reference to update the actual web page.

When a component is rendered, the virtual DOM calculates the difference between the new state and the previous state (a process called "diffing") and makes the minimal set of changes to the real DOM to bring it in sync with the updated virtual DOM (a process called "reconciliation").

but the issue with virtual dom is, if diffing depends on the size of tree, which increases the complexity for big component tree, where only few things are changed but it will compare the whole tree

after virtual dom is overhead movement, new framework came, which don't use virtual dom at all, examples svelte, solid js..., svelte uses dirty checking(), and solid uses same but, it only update very part which is changed in dom, they use direct dom manipulation,

how dirty checking works:

1. The framework keeps track of the initial state of the numbers.
2. Whenever an action, like clicking a button, occurs, the framework checks if any of the numbers have changed since the last time it looked.
3. If a number has changed, the framework updates only that specific part of the screen, showing the new value.
4. If no numbers have changed, the framework doesn't do anything, saving time and resources.





