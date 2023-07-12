# Setting up your local frontend environment
A step-by-step guide to setting up the VA.gov frontend environment locally.
## Step 1: Set up Node
1. Install `nvm`:

   Please follow instructions in the [nvm documentation](https://github.com/nvm-sh/nvm#installing-and-updating) for installing this dependency.
2. Install `node 14.15.0` (this also installs `npm`):
   ```bash
   nvm install 14.15.0
   ```
3. Configure `nvm` to use `node 14.15.0` by default:
   ```bash
   nvm alias default 14.15.0
   ```
4. Install `yarn 1.19.1` globally:
   ```bash
   npm i -g yarn@1.19.1
   ```
5. Verify correct versions of `node` and `yarn` are installed:
   ```bash
   node --version # 14.15.0
   yarn --version # 1.19.1
   ```
## Step 2: Get the source code
Clone VA.gov git repos as **sibling directories**:
```bash
git clone git@github.com:department-of-veterans-affairs/vets-website.git
git clone git@github.com:department-of-veterans-affairs/vagov-content.git
git clone git@github.com:department-of-veterans-affairs/content-build.git
git clone git@github.com:department-of-veterans-affairs/vets-json-schema.git
git clone git@github.com:department-of-veterans-affairs/veteran-facing-services-tools.git
git clone git@github.com:department-of-veterans-affairs/vets-api.git
git clone git@github.com:department-of-veterans-affairs/vets-api-mockdata.git
```
### Front end repos
- `vets-website`: Core front end platform and application code
- `vagov-content`: Markdown content used to generate static pages
- `content-build`: Liquid templates and content build for static pages
- `veteran-facing-services-tools`: Shared front end components (including non VA.gov users) and front end documentation site
### Back end repos
- `vets-api`: Core Rails API server application code
- `vets-api-mockdata`: Mock data used when running locally and on dev for the backend
### Shared repos
- `vets-json-schema`: Shared JSON Schema definitions used by form applications and the APIs that they consume
## Step 3: Start up the front end
### vets-website
1. Navigate to the `vets-website` repository, then install `vets-website` dependencies. See these common commands for more information.
   ```bash
   cd vets-website
   yarn install
   ```
2. Build **all applications** for `vets-website`. Run this standard build script if you need all the CSS and JS generated for work in `content-build`.
   ```bash
   yarn build
   ```

   If you are only working in an [Isolated application(s)](https://depo-platform-documentation.scrollhelp.site/developer-docs/isolated-application-builds) (or do not need to build all applications), you can build **one or more application(s)** with the --entry option.
   ```bash
   yarn build --entry=static-pages,auth
   ```
3. Start the local development server for **all applications**. If you are applying CSS and/or JS changes to a static page/template that renders in `content-build`, we recommend leaving this command running so you will be able to see the changes in `content-build`.
   ```bash
   yarn watch
   ```
   Again, you can limit the watch to one or more application(s) with the --entry option.
   ```bash
   yarn watch --env entry=static-pages,auth
   ```
   The watch is complete when the CLI says `Compiled successfully`.

   If you would like webpack to open a browser window for you, please run `yarn watch --open`. We use [Webpack DevServer](https://webpack.js.org/configuration/dev-server/) to watch and serve the files locally; all the same options and documentation should apply.
4. Open http://localhost:3001 in a browser if you are working on an app; otherwise, continue on to the content-build section for viewing changes in the browser.
> **Note:** You can learn more about building applications in the vets-website GitHub readme.
