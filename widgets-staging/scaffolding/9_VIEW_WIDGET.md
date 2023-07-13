---
permalink: /widgets-staging/scaffolding/view-widget
---

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

>  **Next Up: Writing Unit Tests**
>
> You're ready to begin testing your widget.

[Continue to Testing](../testing/1_START.md)

[Back](./8_CREATE_WIDGET.md)
