---
previous: /widgets/scaffolding/6-mount-widget
next: /widgets/scaffolding/8-view-widget
---

# Call the Widget's "Create" Function

Update the `src/applications/static-pages/static-pages-entry.js` file by importing your new `createHelloWorldWidget` function, and calling it:

```javascript
import { createHelloWorldWidget } from "./hello-world/createHelloWorldWidget";

// Other widget create calls...

createHelloWorldWidget();
```

This step ensures your new widget's "create" function is called on every static content page, giving your widget a chance to mount itself.

Your widget is now scaffolded!
