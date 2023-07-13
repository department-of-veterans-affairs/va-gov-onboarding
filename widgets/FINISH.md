---
permalink: /widgets/finish
---

#   Tutorial: Make a New VA.gov React Widget - Finish

##  Mount to an Existing Page

Running `vets-website` to interact with your widget is a great way to develop your widget in your development environment.

However, for production, your widget should be mounted to an existing page.

1.  Find the Liquid template that is responsible for rendering the existing page.
1.  If there is no specific template for the page, you can assume there is a generic template rendering the page that already is setup to render widgets. In this case, you can add a widget to the existing page in Drupal or `vagov-content` with your widget's unique `widgetType` value.
1.  If there is a specific template for the page, add a `<div>` to the template with a `data-widget-type` attribute whose value is equal to your widget's unique `widgetType`.
