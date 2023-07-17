---
permalink: /widgets/scaffolding/mount-widget
previous: /widgets/scaffolding/create-component
next: /widgets/scaffolding/create-widget
---

# Conditionally Mount the Widget

Create a file for the widget's "create" function.

```sh
touch src/applications/static-pages/hello-world/createHelloWorldWidget.js
```

Add the following contents to the file:

```jsx
import React from "react";
import ReactDOM from "react-dom";
import widgetTypes from "../widgetTypes";

export const createHelloWorldWidget = async () => {
  const container = document.querySelector(
    `div[data-widget-type="${widgetTypes.HELLO_WORLD}"]`
  );
  if (!container) {
    return;
  }

  const { HelloWorldWidget } = await import(
    /* webpackChunkName: "hello-world" */ "./components/HelloWorldWidget"
  );
  ReactDOM.render(<HelloWorldWidget />, container);
};
```

The above code:

1.  Exports a single function called `createHelloWorldWidget`
1.  This function searches for a `<div>` with the `data-widget-type` attribute whose value is the unique string you added to the `widgetTypes` object (`HELLO_WORLD`)
1.  If the `<div>` is not found, the function does nothing
1.  Otherwise, the function imports the `HelloWorldWidget` bundle, which contains the `HelloWorldWidget` React component, and then mounts the component into the `<div>`.
