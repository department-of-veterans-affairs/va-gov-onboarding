---
permalink: /widgets-staging/scaffolding/create-widget
---

##  Call the Widget's "create" Function

Update the `src/applications/static-pages/static-pages-entry.js` file by importing your new `createHelloWorldWidget` function, and calling it:

```javascript
import { createHelloWorldWidget } from './hello-world/createHelloWorldWidget';

// Other widget create calls...

createHelloWorldWidget();
```

This step ensures your new widget's "create" function is called on every page, giving your widget a chance to mount itself.

> **Scaffold Complete!**
>
> Your widget is now scaffolded!

[Continue](./9_VIEW_WIDGET.md)

[Back](./7_MOUNT_WIDGET.md)
