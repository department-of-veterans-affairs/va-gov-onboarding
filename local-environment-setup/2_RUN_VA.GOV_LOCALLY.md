# RUNNING VA.GOV LOCALLY
## What the watch task does
```bash
yarn watch
```
1. Build
  - `vets-website`
    - **Webpack** manages this build pipeline. At a high level, this process:
      - Starts **Webpack**'s development server which
        - **Builds** the **JavaScript** and **CSS** bundles
        - **Serves** the **JavaScript** and **CSS** bundles built by Webpack as well as any scaffolded application pages http://localhost:3001
  - content-build
    - **Metalsmith** manages this build pipeline. At a high level, this process:
      - Retrieves and **builds** all of the **static pages** sourced from `vagov-content` or Drupal
      - **Serves** the **static content** built by Metalsmith at http://localhost:3002
     
2. Output
   - **Metalsmith** in the `content-build` repository outputs **static pages** to `build/localhost`
   - **Webpack** in the `vets-website` repository development server has **no output**. **JavaScript** and **CSS** are kept on disk.

3. Watch and rebuild
   - **Metalsmith** in the `content-build` repository will rebuild **static pages** when changes are saved to **templates** or content in vagov-content
   - **Webpack** in the `vets-website` repository will rebuild when changes are saved to **JavaScript** or **SCSS**
   - Both updates require a browser refresh to see changes.
   - Changes to build process or configuration files are typically not picked up, and require a restart of the watch task to become active.


