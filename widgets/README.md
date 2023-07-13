---
permalink: /widgets/readme
---

#   Tutorial: Make a New VA.gov React Widget - Introduction

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

A VA.gov React Widget ("Widget") is a small React component that is mounted into a `<div>` on a static content page. A static content page is an HTML page whose content is provided by a Content Management System (CMS). While a VA.gov "Application" fills an entire page between the header and footer of VA.gov, a "Widget" only fills in a subsection of the page, allowing developers to include dynamic content into the page without changing the entire application itself.

##  The Static-Pages Application

Within `vets-website` there is an application called `static-pages`. Widgets are defined in subdirectories of the `static-pages` application.

`static-pages` is not like other applications: it does not produce a single-page application that lives between the header and footer of VA.gov. Instead, it produces a JavaScript bundle called `static-pages.entry.js` that is loaded into every static content page on VA.gov. This bundle contains logic that allows each widget to decide whether or not to load themselves into that page using the "conditional widget mounting" pattern.

##  The Conditional Widget Mounting Pattern

Widgets are conditionally mounted into a `<div>` on a static content page using a standardized conditional mounting pattern.

These are the steps to implement the pattern:

1.  Each widget implements a "create" function that searches for a `<div>` based on a unique, `data-widget-type` attribute value, e.g.: `<div data-widget-type="hello-world"/>`.
    *  If the `<div>` is not found the function does not mount the widget
    *  Otherwise, the function loads the widget's bundle and then mounts the widget
1.  The `static-pages` application is responsible for calling every widget's "create" function
1.  The `static-pages.entry.js` bundle is loaded on every static content page

##  Next Up: Scaffold a Widget

You're ready to begin building your widget. You'll start by scaffolding it, by implementing the conditional widget mounting pattern.

[Continue to Scaffolding](./SCAFFOLDING.md)
