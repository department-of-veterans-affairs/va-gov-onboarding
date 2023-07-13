---
permalink: /widgets-staging/scaffolding/create-component
---

##  Create a Basic React Component

Create a file in the `hello-world/components` directory called `HelloWorldWidget.jsx` with the following contents:

```javascript
export const HelloWorldWidget = () => {
  return 'Hello World!';
};
```

This is a basic React component that you'll eventually expand upon to make it do something useful for veterans. A widget can be made up of one or more React components, but this is the top-level component which will dictate how all the other components interact with each other.

[Continue](./7_MOUNT_WIDGET.md)

[Back](./5_COMPONENT_DIR.md)
