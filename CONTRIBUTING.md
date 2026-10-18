# Contributing to RepoQuest

Thanks for your interest in RepoQuest! Bug reports, ideas, docs fixes, and code are all welcome.

## Ways to help

- **Report a bug** – open an issue with the repo URL you tried, what you expected, and what happened (a screenshot helps).
- **Suggest an improvement** – open an issue describing the problem first, then the idea.
- **Pick up an issue** – look for [`good first issue`](../../labels/good%20first%20issue) or [`help wanted`](../../labels/help%20wanted). Comment on the issue so nobody duplicates work.

## Project layout

| Path | What it is |
| --- | --- |
| `frontend/` | Next.js + React + TypeScript app (UI and the `/api/generate` route) |
| `workflows/` | n8n workflow export that fetches GitHub evidence and calls Gemini |

## Local setup

1. Fork and clone the repo.
2. Install and configure the frontend:

   ```bash
   cd frontend
   npm install
   echo "N8N_WEBHOOK_URL=http://127.0.0.1:5678/webhook/repoquest" > .env.local
   ```

3. Start n8n, import the workflow from `workflows/`, and add your GitHub and Gemini credentials inside n8n.
4. Run the app:

   ```bash
   npm run dev
   ```

5. Open http://localhost:3000.

UI-only changes (layout, CSS, components) don't need real credentials if you work against saved sample data, but generating a questline does.

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
- Never commit secrets: API keys, n8n credentials, or `.env*` files.
- If you change the n8n workflow, re-export it to `workflows/` and remove any credential values from the JSON.
- Be kind and constructive in issues and reviews.

## Questions

Not sure where to start? Open an issue titled "Question: ..." and we'll point you in the right direction.
