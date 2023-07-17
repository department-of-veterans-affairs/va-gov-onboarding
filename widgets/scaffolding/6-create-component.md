---
permalink: /widgets/scaffolding/create-component
previous: /widgets/scaffolding/component-directory
next: /widgets/scaffolding/mount-widget
---

# Create a Basic React Component

Create a file for the React component.

```sh
touch src/applications/static-pages/hello-world/components/HelloWorldWidget.jsx
```

Add the following contents to the file:

```javascript
export const HelloWorldWidget = () => {
  return "Hello World!";
};
```

This is a basic React component that you'll eventually expand upon to make it do something useful for veterans.
