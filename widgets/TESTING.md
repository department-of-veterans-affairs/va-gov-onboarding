#   Tutorial: Make a New VA.gov React Widget - Testing

##  Run Locally

You can run `vets-website` locally and interact with your widget. It doesn't do much yet, but after validating the Hello World functionality, you can focus your energy enhancing the React component to implement behavior that will add real value -- the rest is done!

##  Register Your Widget for Local Testing

Update the `src/applications/registry.scaffold.json` file with a new entry for your widget, so that you can run `vets-website` and interact with your widget:

```json
{
"appName": "Hello World Widget",
"rootUrl": "/hello-world",
"widgetType": "hello-world"
}
```

##  Run `vets-website`

```sh
yarn watch
```

##  Interact with Your Widget

Open a browser, and browse to http://localhost:3001/hello-world

You should see the VA.gov header and footer, with your widget in between declaring "Hello World!"

##  Mount to an Existing Page

Running `vets-website` to interact with your widget is a great way to develop your widget in your development environment. However, for production, your widget should be mounted to an existing page.

1.  Find the Liquid template that is responsible for rendering the existing page.
1.  If there is no specific template for the page, you can assume there is a generic template rendering the page that already is setup to render widgets. In this case, you can add a widget to the existing page in Drupal or `vagov-content` with your widget's unique `widgetType` value.
1.  If there is a specific template for the page, add a `<div>` to the template with a `data-widget-type` attribute whose value is equal to your widget's unique `widgetType`.