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

   If you are only working in an [Isolated application(s)](https://depo-platform-documentation.scrollhelp.site/developer-docs/isolated-application-builds) (or do not need to build all applications), you can build one or more application(s) with the --entry option.
