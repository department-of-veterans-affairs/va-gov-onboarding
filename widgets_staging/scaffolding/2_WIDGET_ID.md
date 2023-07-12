#  Add a New Widget Identifier

Add your widget identifier to the JavaScript object defined in  `src/applications/static-pages/widgetTypes.js`. This file contains a list of all widget identifiers.

Follow the convention by adding your new entry in alphabetical order:

```javascript
HELLO_WORLD: 'hello-world'
```

This value will be used by the widget's "create" function to search for a `<div>` with a `data-widget-type` attribute with the value `hello-world`, e.g.: `<div data-widget-type="hello-world"/>`
