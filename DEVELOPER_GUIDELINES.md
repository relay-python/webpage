# Developer Guidelines

These guidelines keep the Relay SDK marketing site consistent and easy to iterate on.

## Tooling

- Use the Hugo **extended** binary (v0.125.0 or newer).
- Optional: use `hugo server --buildDrafts` for live reload while editing content or layouts.

## Workflow

1. Branch from `main`.
2. Update content in `content/_index.md` or create additional sections under `content/` as needed.
3. Modify layouts or styling in `layouts/` to support new sections rather than inlining HTML inside Markdown.
4. Run `hugo --minify` to ensure the build succeeds before pushing.
5. Open a pull request with a short summary of the change and attach screenshots for major UI updates.

## Style Notes

- Keep copy concise and user-focused; link back to the SDK README for deeper dives.
- Prefer semantic HTML tags in layouts; avoid unnecessary `div` wrappers.
- Use the existing design tokens in `layouts/_default/baseof.html` when adding new components to maintain visual consistency.
- Limit inline CSS tweaks inside templates—if you need additional styles, add them near related selectors to keep the stylesheet cohesive.

## Deployment

Pushes to `main` run the GitHub Actions workflow in `.github/workflows/gh-pages.yml`. The workflow:

1. Builds the site with the latest Hugo release.
2. Publishes static assets to the `gh-pages` branch using the GitHub Pages Deploy action.

Verify that a PR build finishes before merging. Once merged, GitHub Pages should serve the updated site within a minute.
