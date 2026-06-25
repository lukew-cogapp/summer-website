## Development

When starting the dev server, use background mode:

```
astro dev --background
```

Manage the background server with `astro dev stop`, `astro dev status`, and `astro dev logs`.

## Deployment

Deployed to GitHub Pages as a **project page** at https://lukew-cogapp.github.io/summer-website/ .

- `.github/workflows/deploy.yml` builds and deploys on every push to `main`.
- `astro.config.mjs` sets `site` and `base: '/summer-website'`. Pages must be public for GitHub Pages on this plan.

### Base-path rule

Because the site is served under `/summer-website/`, **never hardcode a root-relative internal link or asset** (`href="/care/"`, `src="/x.svg"`). They resolve against the domain root and 404 in production.

Prefix internal paths with the configured base. Both `Layout.astro` and `index.astro` define:

```ts
const base = import.meta.env.BASE_URL
const withBase = (p: string) => `${base.replace(/\/$/, '')}${p}`
```

Use `withBase('/care/')` for links and `new URL(withBase(path), Astro.site)` for absolute (canonical/OG) URLs.

## SEO / metadata

`Layout.astro` renders the full `<head>`: title, description, canonical, Open Graph and Twitter cards, `theme-color`. Each page passes a unique `title` and `description` (and optional `ogImage`) as props. Titles self-brand (e.g. `Summer — Care`), so the layout uses them as-is.

## Documentation

Full documentation: https://docs.astro.build

Consult these guides before working on related tasks:

- [Adding pages, dynamic routes, or middleware](https://docs.astro.build/en/guides/routing/)
- [Working with Astro components](https://docs.astro.build/en/basics/astro-components/)
- [Using React, Vue, Svelte, or other framework components](https://docs.astro.build/en/guides/framework-components/)
- [Adding or managing content](https://docs.astro.build/en/guides/content-collections/)
- [Adding styles or using Tailwind](https://docs.astro.build/en/guides/styling/)
- [Supporting multiple languages](https://docs.astro.build/en/guides/internationalization/)
