---
permalink: /widgets/scaffolding/mount-widget
---

## Conditionally Mount the Widget

Create a new file called `createHelloWorldWidget.js` in the widget's root directory (`src/applications/static-pages/hello-world`) with the following content:

```javascript
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
2.  This function searches for a `<div>` with the `data-widget-type` attribute whose value is the unique string you added to the `widgetTypes` object (`HELLO_WORLD`)
3.  If the `<div>` is not found, the function does nothing
4.  Otherwise, the function imports the `HelloWorldWidget` bundle, which contains the `HelloWorldWidget` React component, and then mounts the component into the `<div>`.

[Continue](./8-create-widget.md)

[Back](./6-create-component.md)
