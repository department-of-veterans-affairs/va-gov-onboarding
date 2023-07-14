---
permalink: /widgets
---

# Tutorial: Make a New VA.gov React Widget - Setup

## Step 1: Install NVM (Node Version Manager)

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

## Step 4: Install Dependencies and Run `vets-website`:

```bash
yarn install
```

```bash
yarn watch --env entry=static-pages
```

To view the app open [http://localhost:3001](http://localhost:3001)

[Continue](./introduction/1-start.md)

[Back](/)
