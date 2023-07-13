---
permalink: /local-environment-setup/tutorial-choice
---

## Choose your own adventure

Congratulations at making it this far. At this point in the onboarding process, you are ready to begin making your first commit! As a front end developer, you will be asked to code many different features for the VA. There are four general categories of features which you will make:

- Applications
- Widgets
- Content Pages
- Forms

Each of these features have a unique process for coding them and their own best practices as well. You should learn the process and best practices as-needed. If you do not know which one(s) you will need for your current role, please familiarize yourself with their definitions below and talk with you product manager to determine which you are most likely to build first.

### Applications

These are Javascript applications, written with React/Redux, that control all of the UI for a page and may have multiple client-side pages. There is a static content page for each of these applications that contains only a header, footer, and div for the React application to mount to. These applications have their own JS bundle and the most flexibility for how to render content for a Veteran to interact with.

Examples of applications include our multi page forms, the claim status tracker app, etc.

### Widgets

On VA.gov, we use the term "widgets" to describe features that implement some kind of dynamic behavior in a contained place on a page. Examples of this include our saved application widgets, which display information about in progress applications a signed-in user may have, which is shown on various static content pages. Typically these widgets are written in React and are lazily loaded in separate bundles from the default static pages JS bundle.

### Content pages

Static content pages are pages that are built through the Metalsmith build process and are static html stored in AWS. If you're reading this site, you're probably not the person who would be addding one of these pages. Typically these pages are added by content editors in the vagov-content repo or in the Drupal CMS. You may, however, be tasked with adding more complex behaviors to these pages, which is discussed later in the widgets section.

### Forms

Forms are a specialized widget which serve to provide a digital experience for filling out existing paper forms. While they can be created as a normal widget, forms have a recommended process of using a Yeomen generator much like you would for an application.

## Time to choose

Please select the tutorial which is most immediately useful to you.

> **Note:**
>
> You can always come back to refamiliarize yourself with a tutorial or to select another tutorial to learn that process.

[Continue](./4_CHOOSE.md)

[Back](./2_RUN_VA.GOV_LOCALLY.md)
