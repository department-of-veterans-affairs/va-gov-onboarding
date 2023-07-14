---
permalink: /local-environment-setup/frontend-environment-setup
---

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

Clone VA.gov git repo as **sibling directories**:

```bash
git clone git@github.com:department-of-veterans-affairs/vets-website.git
```
### Front end repos

- `vets-website`: Core front end platform and application code

## Step 3: Start up the front end

### vets-website

1. Navigate to the `vets-website` repository, then install `vets-website` dependencies. See these common commands for more information.
   ```bash
   cd vets-website
   yarn install
   ```
   
2. Build the `vets-website`.
   ```bash
   yarn build
   ```
   
3. Start the local development server. 
   ```bash
   yarn watch
   ```
   
   The watch is complete when the CLI says `Compiled successfully`.

   If you would like webpack to open a browser window for you, please run `yarn watch --open`. We use [Webpack DevServer](https://webpack.js.org/configuration/dev-server/) to watch and serve the files locally; all the same options and documentation should apply.
4. Open http://localhost:3001 in a browser if you are working on an app; otherwise, continue on to the content-build section for viewing changes in the browser.
> **Note:** You can learn more about building applications in the `vets-website` [GitHub readme](https://github.com/department-of-veterans-affairs/vets-website/blob/main/README.md#building-applications).

[Continue](./2_RUN_VA.GOV_LOCALLY.md)

[Back](../platform-overview/5_COMMUNICATION_NORMS.md)
