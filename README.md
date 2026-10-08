# Kostas Antonakoglou

A personal blog built with the official Astro blog template. Includes 51
published posts migrated from WordPress, local image optimization, RSS, and a sitemap.

## Development

Requires Node 22.12 or newer; `.node-version` selects Node 22.23.3.

```bash
npm ci
npm run dev
npm run build
```

Posts live in `src/content/blog/` and local images in `src/assets/images/`.
The production build is generated in `dist/` and is not committed.

## Authoring Posts

Both `.md` and `.mdx` files are supported in `src/content/blog/`; MDX is already
installed and configured. Existing Markdown posts do not need conversion.

Use `image` or `heroImage` in frontmatter for a local article image. If both are
present, `heroImage` takes precedence. The selected image is used for the article,
listing thumbnail, structured data, and social preview:

```yaml
title: "Research notes"
description: "A concise description of the research."
pubDate: "2026-10-08"
image: "../../assets/images/2025/02/nephio_architecture_drawing.png"
```

Without an article image, social previews use the author's portrait. Open Graph
and Twitter metadata use the configured public domain, not the preview server.
Shared pages use Astro's `ClientRouter` for crossfade navigation, including
reduced-motion support.

MDX can import existing Astro components, for example:

```mdx
import FormattedDate from '../../components/FormattedDate.astro';

<FormattedDate date={new Date('2026-10-08T00:00:00.000Z')} />
```

For interactive React charts, install `@astrojs/react` with `npx astro add react`
when needed, then import the React component into an MDX post and use a hydration
directive such as `client:visible`. MDX alone does not install React.

## Cloudflare Pages

Connect this GitHub repository to a Cloudflare Pages project:

- Production branch: `main`
- Framework preset: Astro
- Root directory: repository root
- Build command: `npm run build`
- Build output directory: `dist`
- Node version: `22.23.3` (set `NODE_VERSION` if needed)

The site is fully static and does not need a Cloudflare SSR adapter.
Canonical URLs use `https://antonakoglou.com`; change `site` in `astro.config.mjs`
if deploying permanently to a different domain.

## Migration Notes

WordPress XML backups, the original media export, and migration helpers are
excluded from Git. Only published posts were imported; private posts and drafts
were not published. Review older WordPress shortcodes and missing/external images
before considering the migration complete. Legacy permalink redirects and
WordPress pages are not included.

## Credit

Based on the official Astro blog template and its Bear Blog-inspired styling.
