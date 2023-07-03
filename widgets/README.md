#   Tutorial: Make a New Widget

*As a* developer  
*I want* to learn how to make a widget  
*so that* I can be a productive team member

**Acceptance Criteria**

1.  A new "Hello World" widget is accessible when I run `vets-website` in my development environment
1.  I am ready to develop a full-featured widget
1.  I am confident the pull request to merge my full-featured widget will be merged

##  Prerequisites

1.  All work will take place in the `vets-website` repository
1.  You should have a cursory understanding of JavaScript, JavaScript bundling, React, and the DOM

##  What is a Widget?

A Widget is a small react application that is mounted to a DOM element on an existing static page. This differs from an "Applicaton," in that an Application represents an entire page between the header and footer of VA.gov.

##  The `static-pages` Application

Within `vets-website` there is an Application called `static-pages`. This Application contains subdirectories in which all code widget is stored.

`static-pages` is not like other Applications: it does not produce a single-page application that lives between the header and footer of VA.gov. Instead, it produces a bundle that is loaded into every page on VA.gov called `static-pages.entry.js`. This bundle includes code that allows each widget to decide whether or not to load themselves into that page using the "conditional mounting" pattern.

##  The "Conditional Mounting" Pattern

Widgets are conditionally mounted to a DOM element on an existing page using a "conditional mounting" pattern.

This pattern is implemented as follows:

1.  Each widget implements a `create` function which looks for a DOM element based on a unqiue, widget-specific attribute value, for example, a `<div data-widget-type=my-widget>`.
    1.  If the DOM element is not found the `create` function returns.
    1.  Otherwise, the `create` function mounts the widget to the DOM element, and imports the widget's bundle.
1.  The `static-pages` entrypoint invokes every widget's `create` function
1.  The `static-pages.entry.js` bundle is added to every page

In summary, every page gives every widget a chance to mount itself. Widgets don't need to know which pages they are associated to, so the dependency is unidirectional (pages depend on widgets, widgets don't depend on pages).

This pattern:
-   Allows for re-usability of widgets across pages
-   Maintains consistency in widget scaffolding
-   Has minimal impact on page load time, since the `static-pages.entry.js` bundle only contains the code to conditionally mount widgets, and not the widget bundles themselves
-   Is simple: widgets try to load themselves on every page

##  Scaffolding a Widget

You will begin development of your new widget by scaffolding a widget, meaning you will implement the conditional mounting pattern. Once you've completed the scaffoling, it's up to you how to develop your widget to meet mission needs.

### Create a Feature Branch

Create a new branch off of `main` to develop your new widget:

```sh
git checkout feature/hello-world-widget
```

### Update `widgetTypes` Enumeration

There is a file `src/applications/static-pages/widgetTypes.js` that contains what is essentially an enumeration of widget names.

Follow the convention by adding a new entry, in alphabetical order:

```javascript
HELLO_WORLD: 'hello-world',
```

This value will be used by the conditional mounting pattern to find a DOM element with an attribute `data-widget-type` whose value is `hello-world`.

### Create a Directory for the Widget

Create a new directory under `src/applications/static-pages/`:

```sh
cd src/applications/static-pages/
mkdir hello-world
```

### Create a Directory for the Widget React Component

```sh
cd hello-world
mkdir components
```

### Create a Basic Widget React Component

Create a file in the `hello-world/components` directory called `HelloWorld.jsx` with the following contents:

```javascript
export const HelloWorld = () => {
  return 'Hello World!';
};
```

This is a minimally-viable React component that returns the string "Hello World". When you build you widget functionality, you'll build it by expanding upon this component to make it do something useful. But for now, this is enough as we consider meeting our tutorial acceptance criteria.

###  Implement the `create` Function

Create a new file called `createHelloWorldWidget.js`:

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import widgetTypes from '../widgetTypes';

export const createHelloWorldWidget = async () => {
const container = document.querySelector(
    `[data-widget-type="${widgetTypes.HELLO_WORLD}"]`,
);
if (!container) {
    return;
}

const {
    HelloWorld,
} = await import(/* webpackChunkName: "HelloWorld" */ './components/HelloWorld');
ReactDOM.render(<HelloWorld />, container);
};
```

This file:
1.  Exports a single function called `createHelloWorldWidget`
1.  The `createHelloWorldWidget` function looks for a DOM element with the attribute `data-widget-type` whose value is equal to the unique string in the `widgetTypes` enumeration (`HELLOWORLD`)
1.  If such a DOM element is not found, the function returns
1.  Otherwise, the function imports the `HelloWorld` widget bundle which contains the `HelloWorld` React component, and mounts the component to the DOM element.

### Invoke the Widget `create` Function

Update the `src/applications/static-pages/static-pages-entry.js` file by importing your new `createHelloWorldWidget` function, and invoking it:

```javascript
import { createHelloWorldWidget } from './hello-world/createHelloWorldWidget';

...

createHelloWorldWidget();
```

This step ensures your new widget `create` function is invoked on every page, giving your widget a chance to mount itself.

Your widget is now scaffolded! ✅

##  Run Locally

You can run `vets-website` locally and interact with your widget. It doesn't do much yet, but after validating the Hello World functionality, you can focus your energy enhancing the React component to implement behavior that will add real value -- the rest is done!

### Register Your Widget for Local Testing

Update the `src/applications/registry.scaffold.json` file with a new entry for your widget, so that you can run `vets-website` and interact with your widget:

```json
{
"appName": "Hello World Widget",
"rootUrl": "/hello-world",
"widgetType": "hello-world"
}
```

### Run `vets-website`

```sh
yarn watch
```

### Interact with Your Widget

Open a browser, and browse to http://localhost:3001/hello-world

You should see the VA.gov header and footer, with your widget in between declaring "Hello World!"

##  Mount to an Existing Page

Running `vets-website` to interact with your widget is a great way to develop your widget in your development environment. However, for production, your widget should be mounted to an existing page.

1.  Find the Liquid template that is responsible for rendering the existing page.
1.  If there is no specific template for the page, you can assume there is a generic template rendering the page that already is setup to render widgets. In this case, you can add a widget to the existing page in Drupal or `vagov-content` with your widget's unique `widgetType` value.
1.  If there is a specific template for the page, add a `<div>` to the template with a `data-widget-type` attribute whose value is equal to your widget's unique `widgetType`.