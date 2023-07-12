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
## Running VA.gov locally for specific environments
> **Note:** Typically, the reason for building the site locally like this is to build it in production mode and check that it is behaving as you'd expect. Most of the time, it's better to use the `watch` task to build the site locally since it is the most developer-friendly experience.

[TABLE INSERT]

### What the build commands do
- **create** the **static pages** from the markdown content in the vagov-content repository and data queried from the Drupal API into their **output directory**.
- **create** the **JavaScript** and **CSS** files with **Webpack** into `/generated` folder in their **output directory** with Webpack.
### What the run commands do
- **start** an `http-server` that **serves** the **static pages** from the **output directory** at http://localhost:3001
### Notes
- Production-like builds are required for staging and production environments. **NODE_ENV=production** environment variable is required to be set when running these build commands
- **Deep-linking** to urls that are rendered by **React** apps on VA.gov **will not work** when you run the site this way, as that relies on some server-side routing that is handled in nginx (or the Webpack dev server when running the `watch` task)
## Running VA.gov locally for specific applications
> **Note:** Use these commands if you are only working in one or more specific application(s) and want to speed up build and watch times. This is highly recommended if your [application(s) is isolated](https://depo-platform-documentation.scrollhelp.site/developer-docs/isolated-application-builds).
### Build one or more application(s) with the --entry option
```sh
$ yarn build --entry=static-pages,auth
```
### Start the local development server for one or more application(s) with the `--entry` option
```sh
yarn watch --env entry=static-pages,auth
```
### Related sources
- [Metalsmith build script](https://github.com/department-of-veterans-affairs/content-build/tree/main/src/site/stages/build)
- [Webpack development server config](https://github.com/department-of-veterans-affairs/vets-website/blob/main/config/webpack.dev.config.js)

