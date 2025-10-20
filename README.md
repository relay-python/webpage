# Relay SDK Website

This repository contains the Hugo-powered marketing site for the [relay-python/relay](https://github.com/relay-python/relay) SDK. It highlights the project’s goals, supported providers, and quick-start snippets so developers can get productive without memorising multiple vendor APIs.

## Getting Started

1. Install [Hugo Extended](https://gohugo.io/getting-started/installing/) (v0.125.0 or newer).
2. Clone the repository and install dependencies (none beyond Hugo itself).
3. Run a local preview server (override the production base URL so assets resolve locally):
   ```bash
   hugo server --buildDrafts --baseURL http://localhost:1313/
   ```
   The site will be available at <http://localhost:1313>.

## Project Layout

- `content/_index.md` – Front-matter driven homepage sections (hero copy, feature cards, provider details, roadmap, etc).
- `layouts/` – Base template and homepage layout with custom styling for the Relay brand.
- `static/` – Place any static assets (images, downloads) you want published as-is.
- `public/` – Generated output; ignored by git because CI builds and deploys it automatically.
- `hugo.toml` – Site configuration, metadata, and params consumed by layouts.

## Contributing

Before opening a pull request:

1. Read the [Developer Guidelines](./DEVELOPER_GUIDELINES.md).
2. Run `hugo --minify` locally to confirm the site builds without warnings.
3. Preview the site (`hugo server`) and sanity-check layout/content changes.

## Deployment

GitHub Actions (defined in `.github/workflows/gh-pages.yml`) builds the site with Hugo and publishes the generated HTML to the `gh-pages` branch. Ensure GitHub Pages is configured to serve from that branch in the repository settings. Pushes to `main` automatically trigger a deploy.
