# RepoQuest frontend

The Next.js app for RepoQuest. See the [root README](../README.md) for the project overview, environment variables, and limitations.

## Run locally

```bash
npm ci
cp .env.example .env.local   # fill in GEMINI_API_KEY (and GITHUB_TOKEN if you have one)
npm run dev
```

Open http://localhost:3000.

## Scripts

| Command | What it does |
| --- | --- |
| `npm run dev` | Start the dev server. |
| `npm run lint` | Run ESLint. |
| `npm run build` | Create a production build. |
| `npm start` | Serve the production build. |

## Layout

| Path | What it is |
| --- | --- |
| `src/app/page.tsx` | The single-page UI: questline, issues, progress, and snapshots. |
| `src/app/api/generate/route.ts` | The pipeline: validate URL, fetch GitHub evidence, call Gemini, validate the result. |
| `src/app/globals.css` | Styles. |

Restart the dev server after changing environment variables.
