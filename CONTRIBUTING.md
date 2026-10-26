# Contributing to RepoQuest

Thanks for your interest in RepoQuest! Bug reports, ideas, docs fixes, and code are all welcome.

## Ways to help

- **Report a bug**: open an issue with the repo URL you tried, what you expected, and what happened (a screenshot helps).
- **Suggest an improvement**: open an issue describing the problem first, then the idea.
- **Pick up an issue**: look for [`good first issue`](https://github.com/infi9itea/repoquest/labels/good%20first%20issue) or [`help wanted`](https://github.com/infi9itea/repoquest/labels/help%20wanted). Comment on the issue so nobody duplicates work.

## Project layout

| Path | What it is |
| --- | --- |
| `frontend/` | The Next.js + React + TypeScript app. |
| `frontend/src/app/api/generate/route.ts` | The whole pipeline: URL validation, GitHub evidence, Gemini call, and response validation. |
| `frontend/src/app/page.tsx` | The UI. |

## Local setup

1. Fork and clone the repo.
2. Install and configure the frontend:

   ```bash
   cd frontend
   npm ci
   cp .env.example .env.local
   ```

3. Put your `GEMINI_API_KEY` in `.env.local`. A `GITHUB_TOKEN` with no extra permissions is optional but avoids GitHub rate limits.
4. Run the app:

   ```bash
   npm run dev
   ```

5. Open http://localhost:3000.

Generating a questline needs a Gemini key. UI-only changes (layout, CSS, components) can be checked against the sample questline shown on first load.

## Making a change

1. Create a branch: `git checkout -b fix/short-description`.
2. Keep the change focused: one fix or feature per pull request.
3. Before pushing, run:

   ```bash
   cd frontend
   npm run lint
   npm run build
   ```

4. For UI changes, check desktop and mobile widths and attach before/after screenshots to the PR.
5. Open a pull request and describe what changed and why. Link the issue (`Closes #123`).

## Guidelines

- Follow the existing code style; the ESLint config is the source of truth.
- Never commit secrets: API keys, tokens, or `.env*` files (only `.env.example` is tracked).
- Treat issue text and model output as untrusted. Keep the validation in `route.ts` strict.
- Be kind and constructive in issues and reviews.

## Questions

Not sure where to start? Open an issue titled "Question: ..." and we'll point you in the right direction.
