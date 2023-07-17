---
previous: /widgets/scaffolding/7-create-widget
next: /widgets/testing
---

# View Your Widget

Before you can see your widget locally, you need to register it in `src/applications/registry.scaffold.json`:

```json
{
  "appName": "Hello World Widget",
  "rootUrl": "/hello-world",
  "widgetType": "hello-world"
}
```

Then run just the `static-pages` application in `vets-website`:

```sh
yarn watch --env entry=static-pages
```

Open [http://localhost:3001/hello-world](http://localhost:3001/hello-world) in your browser. You should see the VA.gov header and footer with your widget in between declaring "Hello World!"

## Next Up: Writing Unit Tests

You're ready to begin testing your widget.
