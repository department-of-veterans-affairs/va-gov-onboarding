---
permalink: /widgets/scaffolding/view-widget
previous: /widgets/scaffolding/create-widget
next: /widgets/testing/start
---

# View Your Widget

Before you can see your widget locally, you need to register it in the `src/applications/registry.scaffold.json` file with a new entry for your widget:

```json
{
  "appName": "Hello World Widget",
  "rootUrl": "/hello-world",
  "widgetType": "hello-world"
}
```

Run just the `static-pages` application in `vets-website`:

```sh
yarn watch --env entry=static-pages
```

Open http://localhost:3001/hello-world in your browser. You should see the VA.gov header and footer with your widget in between declaring "Hello World!"

## Next Up: Writing Unit Tests

You're ready to begin testing your widget.
