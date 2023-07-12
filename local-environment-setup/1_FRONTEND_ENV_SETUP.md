# Setting up your local front-end environment
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
> **Note:** You can learn more about building applications in the `vets-website` [GitHub readme](https://github.com/department-of-veterans-affairs/vets-website/blob/main/README.md#building-applications).
### content-build
> **Note:** In order to run `content-build`, you must first generate the CSS and JS files within `vets-website` (follow steps above). If you don't, you will see a build error in the console instructing you to first generate files in `vets-website`. If you are applying CSS and/or JS changes to a static page/template that renders in `content-build` (like the homepage) you will need to run a watch in `vet-website` to view the updates. The CSS and JS files within `vets-website` are locally connected through a symlink in the build process.
If you don't need to locally view static pages and are just working on applications, you don't need to set this part up.
1. Navigate to the `content-build` repository, then install dependencies via `yarn`.
   ```bash
   cd content-build
   yarn install
   ```
2. Content-build steps requires an additional set up step due to code changes in the app. If building content from Drupal, it requires a one-time setup of a `.env` file to supply connection information.
   ```bash
   cp .env.example .env
   ```
3. Build `content-build`. Make sure you configured the [SOCKS proxy](https://depo-platform-documentation.scrollhelp.site/getting-started/accessing-internal-tools-via-socks-proxy) to fetch content from Drupal. For a faster installation, use step 4 first.
   ```bash
   yarn build
   ```
4. If you do not have access to the SOCKS proxy, you can alternately fetch the latest cached version of the content.
   ```bash
   yarn fetch-drupal-cache
   ```
5. Start the local development server.
   ```bash
   yarn watch
   ```
6. The watch is complete when the CLI says `Compiled successfully`. If you just need a server running without watching the metalsmith files you can `run npx http-server . -p 3002` inside `/build/localhost` to save some CPU.
7. Open http://localhost:3002 in a browser.
## Step 4: Backend and internal tools set up
Setting up the backend and internal tools allows local test account login and static content rendering.
- [Backend](https://github.com/department-of-veterans-affairs/vets-api) (`vets-api`) set up instructions

  The local `vets-website` is configured to point to the `vets-api` backend at `http://localhost:3000`. Any website functionality that depends on the backend (i.e. login, save-in-progress, form submission, feature toggles) will require a locally running instance of `vets-api`.

- [Local test account login instructions](https://github.com/department-of-veterans-affairs/va.gov-team-sensitive/blob/master/Administrative/accessing-staging.md)

- [Internal tools setup instructions](https://depo-platform-documentation.scrollhelp.site/getting-started/Internal-tools-access-via-SOCKS-proxy.1821081710.html)

  This proxy setup is required to access static content locally and to access to our reporting and monitoring tools. Running the yarn watch task with the SOCKS proxy active will automatically pull and cache the static content for vets-website.
