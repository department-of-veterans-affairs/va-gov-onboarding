---
permalink: /widgets/introduction/static-pages
previous: /widgets/introduction/widget
next: /widgets/introduction/conditional-mounting
---

# The static-pages Application

Within `vets-website` there is an application called `static-pages`. Widgets are defined in subdirectories of the `static-pages` application.

`static-pages` is not like other applications: it does not produce a single-page application that lives between the header and footer of VA.gov. Instead, it produces a JavaScript bundle called `static-pages.entry.js` that is loaded into every static content page on VA.gov. This bundle contains logic that allows each widget to decide whether or not to load themselves into that page using the "conditional widget mounting" pattern.
