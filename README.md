# RepoQuest

**An AI-assisted guide to exploring unfamiliar codebases.**

RepoQuest turns a public GitHub repository into three guided developer quests. Each quest has an investigation goal, concrete steps, success criteria, and links to real GitHub issues and likely source files.

**Live demo:** https://repo-quest-five.vercel.app

## Features

- Generate quests from any public GitHub repository.
- Quests are built from repository metadata, recent open issues, and a source-file path index.
- Links point to real issues and to file paths that exist in the repository.
- Works for repositories with no open issues.
- Track quest progress and save workspace snapshots in your browser.

## How it works

1. The Next.js route `/api/generate` accepts only `https://github.com/owner/repo` URLs and rate limits requests per IP.
2. It fetches repository metadata, the five most recently updated open issues, and a ranked index of source-file paths from the GitHub REST API.
3. It sends that evidence to Google Gemini and asks for exactly three quests as JSON.
4. The response is validated before it reaches the UI: issue numbers must exist in the fetched data, issue URLs come from GitHub rather than the model, and file paths must appear in the fetched index.
5. Progress and saved snapshots are stored in your browser (`localStorage`).

```text
Browser  ->  /api/generate (Next.js)  ->  GitHub REST API
                    |
                    +-------------------->  Gemini API
```

## Tech stack

Next.js, React, TypeScript, the GitHub REST API, and the Google Gemini API.

## Getting started

You need a current LTS version of Node.js and a Gemini API key.

```bash
cd frontend
npm ci
cp .env.example .env.local   # then fill in your keys
npm run dev
```

Open http://localhost:3000.

| Variable | Required | Purpose |
| --- | --- | --- |
| `GEMINI_API_KEY` | Yes | Gemini API key used to generate quests. |
| `GITHUB_TOKEN` | Recommended | GitHub token with no extra permissions. Raises GitHub API rate limits. |
| `GEMINI_MODEL` | No | Override the default Gemini model. |
| `RATE_LIMIT_PER_HOUR` | No | Requests allowed per IP per hour (default 10). |

Never commit `.env*` files or tokens.

## Deploying

The app deploys to Vercel with the root directory set to `frontend`. Add the variables above in the Vercel project settings.

## Limitations

- Only public repositories are supported.
- Quests use a small slice of evidence: five open issues and file paths, not file contents. Check the code before trusting a quest.
- Path validation proves a file exists, not that it implements the behavior a quest describes.
- The rate limiter is in memory and resets on cold starts.

## Support

Questions or bugs: open an [issue](https://github.com/infi9itea/repoquest/issues) or email educational006006@gmail.com.

## Built on the GitHub API

   <picture>
     <source media="(prefers-color-scheme: dark)" srcset="docs/GitHub_Invertocat_White.svg">
     <img src="docs/github_Invertocat_Black.svg" alt="GitHub" height="20">
   </picture>

   RepoQuest uses the GitHub REST API for repository metadata, issues, and file trees. It is an independent project and is not endorsed by GitHub.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md).

## Security

Keep API keys and tokens out of source control. To report a vulnerability, email educational006006@gmail.com instead of opening a public issue.

## Project status

Working prototype. Quest quality depends on the evidence available for each repository.

**Development note:** AI coding tools were used to assist with parts of development, including debugging and implementation. I reviewed and tested the resulting code and take responsibility for the project's functionality.

## License

MIT. See [LICENSE](LICENSE).
