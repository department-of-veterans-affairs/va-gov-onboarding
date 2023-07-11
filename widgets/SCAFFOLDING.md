#   Tutorial: Make a New VA.gov React Widget - Scaffolding

All work will take place within the `vets-website` repository.

##  Create a Feature Branch

Create a new branch off of `main` to develop your new widget:

```sh
git checkout -b feature/hello-world-widget
```

##  Add a New Widget Identifier

Add your widget identifier to the JavaScript object defined in  `src/applications/static-pages/widgetTypes.js`. This file contains a list of all widget identifiers.

Follow the convention by adding your new entry in alphabetical order:

```javascript
HELLO_WORLD: 'hello-world'
```

This value will be used by the widget's "create" function to search for a `<div>` with a `data-widget-type` attribute with the value `hello-world`, e.g.: `<div data-widget-type="hello-world"/>`

##  Create a Directory for the Widget

Create a new directory under the `static-pages` application:

```sh
cd src/applications/static-pages/
mkdir hello-world
```

##  Create a Directory for the React Component

Create a new directory under the `hello-world` widget directory:

```sh
cd hello-world
mkdir components
```

##  Create a Basic React Component

Create a file in the `hello-world/components` directory called `HelloWorldWidget.jsx` with the following contents:

```javascript
export const HelloWorldWidget = () => {
  return 'Hello World!';
};
```

This is a basic React component that you'll eventually expand upon to make it do something useful for veterans. A widget can be made up of one or more React components.

##  Conditionally Mount the Widget

Create a new file called `createHelloWorldWidget.js` in the widget's root directory (`src/applications/static-pages/hello-world`) with the following content:

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import widgetTypes from '../widgetTypes';

export const createHelloWorldWidget = async () => {
  const container = document.querySelector(
    `div[data-widget-type="${widgetTypes.HELLO_WORLD}"]`,
  );
  if (!container) {
      return;
  }

  const { HelloWorldWidget } =
      await import(/* webpackChunkName: "hello-world" */ './components/HelloWorldWidget');
  ReactDOM.render(<HelloWorldWidget/>, container);
};
```

The above code:
1.  Exports a single function called `createHelloWorldWidget`
1.  This function searches for a `<div>` with the `data-widget-type` attribute whose value is the unique string you added to the `widgetTypes` object (`HELLO_WORLD`)
1.  If the `<div>` is not found, the function does nothing
1.  Otherwise, the function imports the `HelloWorldWidget` bundle, which contains the `HelloWorldWidget` React component, and then mounts the component into the `<div>`.

##  Call the Widget's "create" Function

Update the `src/applications/static-pages/static-pages-entry.js` file by importing your new `createHelloWorldWidget` function, and calling it:

```javascript
import { createHelloWorldWidget } from './hello-world/createHelloWorldWidget';

// Other widget create calls...

createHelloWorldWidget();
```

This step ensures your new widget's "create" function is called on every page, giving your widget a chance to mount itself.

Your widget is now scaffolded!

##  View Your Widget

Before you can see your widget locally, you need to register it in the `src/applications/registry.scaffold.json` file with a new entry for your widget:

```json
{
  "appName": "Hello World Widget",
  "rootUrl": "/hello-world",
  "widgetType": "hello-world"
}
```

Run `vets-website`:

```sh
yarn watch --env entry=static-pages
```

Open http://localhost:3001/hello-world in your browser. You should see the VA.gov header and footer with your widget in between declaring "Hello World!"

##  Next Up: Writing Unit Tests

You're ready to begin testing your widget.

[Continue to Testing](./TESTING.md)
