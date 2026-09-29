# Patterns notebook

A mobile-first quick reference for C# and TypeScript. Pages are short on purpose: syntax reminders and common patterns, not tutorials.

The site is markdown rendered in the browser with [Docsify](https://docsify.js.org) (no build step) and published with GitHub Pages.

**Live site:** https://atamburino.github.io/patterns-notebook/

## Layout

| Path | What it is |
| --- | --- |
| `docs/index.html` | Docsify shell, theme, and search |
| `docs/README.md` | Home page |
| `docs/_navbar.md` | Home / C# / TypeScript links |
| `docs/_sidebar.md` | Side navigation for every pattern page |
| `docs/csharp/` | C# notes |
| `docs/typescript/` | TypeScript notes |
| `docs/assets/site.css` | Mobile-first theme (light, and dark when the OS asks) |

GitHub Pages serves the `docs/` folder on `main`. `.nojekyll` is in that folder so Jekyll does not drop `_sidebar.md` and `_navbar.md`.

## Add a page

1. Add a markdown file under `docs/csharp/` or `docs/typescript/`.
2. Keep it short: a few fenced snippets and one to three gotchas. Fence C# as `csharp` and TypeScript as `ts`.
3. Link it from `docs/_sidebar.md`, indented under that language.
4. Link it from that language's `README.md` (`docs/csharp/README.md` or `docs/typescript/README.md`) so the section overview stays complete.
5. Commit to `main`. Pages republishes the `docs/` folder; there is nothing to compile.

Write links from the site root, for example `[Null handling](/csharp/null-handling.md)`. Docsify turns those into routes. The address bar uses a hash (`/#/csharp/null-handling`), which works on GitHub project pages without extra redirects.

## Preview locally

From the repo root:

```bash
python3 -m http.server 8080 --directory docs
```

Open http://localhost:8080/ and use the top links to move between Home, C#, and TypeScript. On a phone-width window, open the menu button at the top left.

## GitHub Pages

Source: **Deploy from a branch** → branch **`main`** → folder **`/docs`**.

The published URL is https://atamburino.github.io/patterns-notebook/

No custom domain is configured. Do not add a `CNAME` file unless you actually have a domain to point here.

If the site is not being served, turn Pages back on:

1. Open this repo on GitHub.
2. Go to **Settings → Pages**.
3. Under **Build and deployment**, set **Source** to **Deploy from a branch**.
4. Set **Branch** to `main` and the folder to `/docs`.
5. Save. The first deploy often takes a minute or two. The Pages settings page shows the URL when it is ready.
