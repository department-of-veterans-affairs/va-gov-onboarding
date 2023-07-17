---
permalink: /widgets/introduction/conditional-mounting
previous: /widgets/introduction/static-pages
next: /widgets/scaffolding/start
---

# The Conditional Widget Mounting Pattern

Widgets are conditionally mounted into a `<div>` on a static content page using a standard pattern:

1.  Each widget implements a "create" function that searches for a `<div>` based on a unique, `data-widget-type` attribute value, e.g.: `<div data-widget-type="hello-world"/>`.

- If the `<div>` is not found the function does not mount the widget
- Otherwise, the function loads the widget's bundle and then mounts the widget

1.  The `static-pages` application is responsible for calling every widget's "create" function
1.  The `static-pages.entry.js` bundle is loaded on every static content page

## Next Up: Scaffolding

You're ready to begin building your widget. You'll start by implementing the conditional widget mounting pattern.
