# woodward-reporting

GOAL reporting for **Woodward Insurance Agency** (Terre Haute, IN), deployed as a
static site on Vercel.

## Contents

| Path | URL | Page |
| --- | --- | --- |
| `index.html` | `/` | Landing page linking to every report |
| `reports/auto-campaign-configuration.html` | `/reports/auto-campaign-configuration` | IN Auto Campaign Configuration |
| `reports/home-campaign-configuration.html` | `/reports/home-campaign-configuration` | IN Home Campaign Configuration |

Every page is a single self-contained HTML file (logos are inlined as base64). The
only external request is the Sora and Outfit webfonts from Google Fonts. There is no
build step and there are no dependencies.

Pages open in the viewer's system light or dark mode. The round toggle in the
top-right corner overrides it, and the choice is shared across every page on the
site (`localStorage` key `goal-theme`). Print is always light.

## Deploying on Vercel

`vercel.json` serves the repo root as a static site:

- `framework: null`, `buildCommand: null`, `outputDirectory: "."` (no build, serve as-is)
- `cleanUrls: true`, so `/reports/<name>` works without `.html` and `.html` links redirect to the clean URL
- `X-Robots-Tag: noindex` plus `robots.txt` keep the client reports out of search engines
- basic security headers (`nosniff`, `SAMEORIGIN`, strict referrer policy)

To deploy: import this repo into Vercel (or `vercel link` from the repo root) with the
Framework Preset left as **Other** and no build or install command. Once connected,
every push to `main` publishes to production and every other branch or PR gets a
preview URL. Import the repo only once, or every push will build in two projects.

## Adding another report

Put the new HTML file in `reports/` with a lowercase, hyphenated name, add a card and
a sidebar link for it in `index.html`, then commit and push.

## Previewing locally

```sh
python3 -m http.server 8000
# then open http://localhost:8000
```
