# Trustworthy and Secure AI Lab (TSAIL)

Static lab website built with Astro. The original visual theme is preserved across seven pages.

## Local development

Use Node.js 24 LTS and npm.

```sh
npm ci
npm run dev
```

To build and preview the production website:

```sh
npm run build
npm run preview
```

Astro generates the deployable website in `dist/`. The source home page is `src/pages/index.astro`; a root-level `index.html` is no longer used.

## Project structure

| Path | Purpose |
| --- | --- |
| `src/pages/` | Home, About, Research, People, Publications, Teaching and Join Us |
| `src/components/` | Shared header and footer |
| `src/layouts/SiteLayout.astro` | Shared document layout |
| `src/styles/global.css` | Shared theme and responsive styles |
| `src/data/people.json` | Student names, research topics and optional portraits |
| `public/images/` | Images served at `/images/` |
| `.github/workflows/deploy.yml` | GitHub Pages build and deployment |

## Adding students and photos

Add an entry to the relevant group's `students` array in `src/data/people.json`:

```json
{ "name": "Full Name", "topic": "Research topic", "photo": "" }
```

The grid adds rows automatically. Groups without students are hidden. Each group needs a unique `id`, a `title` and a `students` array.

To add a portrait, create `public/images/students/`, put the image there and set `photo` to `/images/students/filename.jpg`. The field is optional. Initials are displayed when no photo is supplied or a photo fails to load. Portraits use a consistent square crop and load lazily.

## What belongs in Git

Commit `src/`, `public/`, `.github/`, `astro.config.mjs`, `tsconfig.json`, `package.json`, `package-lock.json`, `.gitignore`, `.gitattributes`, this README and the license. Keep the lockfile: CI uses `npm ci` for repeatable dependency installation.

Do not commit `node_modules/`, `dist/`, `.astro/`, environment files, logs or local machine settings. These are excluded by `.gitignore`. Only an intentionally sanitized `.env.example` may be tracked.

The migration removes the old root `index.html` and relocates the old `images/` files into `public/images/`. Include those removals when committing; do not keep a second copy of the old website.

## GitHub Pages

In **Settings > Pages**, select **GitHub Actions** as the deployment source. The workflow builds and deploys on pushes to `main` and supports manual runs. No generated HTML needs to be committed.

The site URL is configured in `astro.config.mjs`. The course website at `https://trustworthy-and-secure-ai-lab.github.io/SPML2026/` is maintained separately.

See the [Astro GitHub Pages guide](https://docs.astro.build/en/guides/deploy/github/).
