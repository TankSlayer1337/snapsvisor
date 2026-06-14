# Snapsvisor

A collection of Swedish *snapsvisor* (drinking songs), published as a website
built with [Docusaurus](https://docusaurus.io/).

**Live site:** https://snapsvisor.org

The site is hosted on GitHub Pages, served from the custom domain
`snapsvisor.org`. The Docusaurus project lives in the [`my-website/`](my-website/)
directory and runs in
[docs-only mode](https://docusaurus.io/docs/docs-introduction#docs-only-mode).

## Prerequisites

- [Node.js](https://nodejs.org/) >= 18
- npm (the project uses npm; a `package-lock.json` is committed)

All commands below are run from the `my-website/` directory:

```bash
cd my-website
```

## Install

```bash
npm install
```

## Local development

```bash
npm run start
```

Starts a local dev server and opens a browser window. Most changes are reflected
live without restarting the server.

## Build

```bash
npm run build
```

Generates static content into the `build/` directory, which can be served by any
static hosting service.

## Deployment

Builds the site and pushes it to the `gh-pages` branch. See the
[Docusaurus deployment docs](https://docusaurus.io/docs/deployment#deploy).

Using SSH:

```bash
USE_SSH=true npm run deploy
```

Not using SSH:

```bash
GIT_USER=TankSlayer1337 npm run deploy
```

### Custom domain

The domain is configured via [`my-website/static/CNAME`](my-website/static/CNAME),
which Docusaurus copies into the build output on every deploy so the
`snapsvisor.org` domain persists. DNS points the apex domain at GitHub Pages
(A/AAAA records), with a `www` CNAME to `tankslayer1337.github.io`.
