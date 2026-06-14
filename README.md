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

The site is served from `snapsvisor.org`, an apex domain whose DNS is managed by
Cloudflare and pointed at GitHub Pages.

**Cloudflare DNS records**

| Type  | Name (host) | Content                  | Proxy status |
| ----- | ----------- | ------------------------ | ------------ |
| A     | `@`         | `185.199.108.153`        | DNS only     |
| A     | `@`         | `185.199.109.153`        | DNS only     |
| A     | `@`         | `185.199.110.153`        | DNS only     |
| A     | `@`         | `185.199.111.153`        | DNS only     |
| AAAA  | `@`         | `2606:50c0:8000::153`    | DNS only     |
| AAAA  | `@`         | `2606:50c0:8001::153`    | DNS only     |
| AAAA  | `@`         | `2606:50c0:8002::153`    | DNS only     |
| AAAA  | `@`         | `2606:50c0:8003::153`    | DNS only     |
| CNAME | `www`       | `tankslayer1337.github.io` | DNS only   |

The four A and four AAAA records are GitHub Pages' published apex addresses. The
`www` CNAME makes `www.snapsvisor.org` resolve to the GitHub Pages host; GitHub
then redirects between `www` and the apex automatically.

> **Important:** all records must be **DNS only** (grey cloud), not proxied
> (orange cloud). This lets GitHub Pages issue and serve its own TLS certificate.
> If the records are proxied, GitHub can't provision a certificate and a
> "Flexible" Cloudflare SSL mode can cause redirect loops.

**GitHub Pages settings** (repo **Settings → Pages**)

- **Custom domain:** `snapsvisor.org`. Saving this writes a `CNAME` file to the
  published branch; it is mirrored by
  [`my-website/static/CNAME`](my-website/static/CNAME), which Docusaurus copies
  into the build output on every deploy so the domain survives redeploys.
- **Enforce HTTPS:** enabled (available once GitHub has issued the certificate,
  which can take up to ~24h after DNS first resolves).
