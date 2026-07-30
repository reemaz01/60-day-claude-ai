# Contributing to codeAgent

Thanks for taking a look at this project. It started as a 10-day capstone build, so contributions are welcome but the codebase is still young — expect some rough edges.

## Getting set up

See the "Running locally" section in [README.md](./README.md). You'll need Node 18+, and either Ollama (for free local LLM calls) or a Gemini API key.

## Before opening a PR

- `cd client && npm run lint` and `npm run build` should both pass
- `cd server && node --check <file>` (or just boot the server) for any changed backend file
- If you touch repository ingestion (`ingestionService.js`), please re-verify the zip-bomb and path-traversal protections still hold — that code exists specifically to reject malicious input, so it's worth extra care

## Reporting issues

Open a GitHub issue with steps to reproduce. If it's a generation-quality issue (the LLM producing bad code), please note which provider you were using (`LLM_PROVIDER=ollama` or `gemini`) and which model — quality varies meaningfully between them.

## Code style

No enforced formatter yet. Match the surrounding file's conventions — this codebase favors small, single-purpose service functions with explicit `err.code`/`err.status` on thrown errors (see any file in `server/src/services/` for the pattern).
