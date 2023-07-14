---
permalink: /local-environment-setup/frontend-environment-setup
---

# Frontend environment setup

## Step 1: Set up NVM (Node Version Manager)

1. Use `nvm` to manage `node`. Follow the [install instructions](https://github.com/nvm-sh/nvm#installing-and-updating).

## Step 2: Clone the VA.gov `vets-website` repository

```bash
git clone git@github.com:department-of-veterans-affairs/vets-website.git
```

## Step 3: Install Node and Yarn

Install `node`:

```bash
cd vets-website
```

```bash
nvm install
```

Install `yarn` globally:

```bash
npm install -g yarn
```

## Step 4: Install dependencies and start the app:

```bash
cd vets-website
```

```bash
yarn install
```

```bash
yarn watch
```

To view the app open [http://localhost:3001](http://localhost:3001)

[Continue](./2-run-va-gov-locally.md)

[Back](/platform-overview/5-communication-norms.md)
