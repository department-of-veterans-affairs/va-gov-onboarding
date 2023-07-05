#   Tutorial: Make a New VA.gov React Widget

*As a* frontend developer  
*I want* to learn how to make a VA.gov React widget  
*so that* I can understand how to build one of the types of features on VA.gov

**Acceptance Criteria**

1.  I can view a new "Hello World" widget when I run `vets-website` locally
1.  I understand how to develop a widget

##  Prerequisites

1.  The `vets-website` repository is cloned locally
1.  Familiarity with JavaScript, JavaScript bundling, React, and the DOM

##  What is a VA.gov React Widget?

A VA.gov React Widget ("Widget") is a small React component that is mounted into a `<div>` on a static content page. A static content page is an HTML page whose content is provided by a Content Management System (CMS). A Widget differs from a VA.gov "Application" which fills an entire page between the header and footer of VA.gov.

##  The Widget Application

Within `vets-website` there is an application called `static-pages`. Widgets are defined in subdirectories of the `static-pages` application.

`static-pages` is not like other applications: it does not produce a single-page application that lives between the header and footer of VA.gov. Instead, it produces a JavaScript bundle called `static-pages.entry.js` that is loaded into every static content page on VA.gov. This bundle contains logic that allows each widget to decide whether or not to load themselves into that page using the "conditional widget mounting" pattern.

##  The Conditional Widget Mounting Pattern

Widgets are conditionally mounted into a `<div>` on a static content page using a standardized conditional mounting pattern.

These are the steps to implement the pattern:

1.  Each widget implements a `create` function that searches for a `<div>` based on a unique, `widget-type` HTML data attribute value, e.g.: `<div data-widget-type="my-widget"/>`.
    *  If the `<div>` is not found the function does not mount the widget
    *  Otherwise, the function loads the widget's bundle and then mounts the widget
1.  The `static-pages` application is responsible for calling every widget's `create` function
1.  The `static-pages.entry.js` bundle is loaded on every static content page

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