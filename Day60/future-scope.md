# codeAgent — Future Scope

A realistic look at where this project could go, grounded in what's actually built today: a session-based (no DB, no auth) pipeline that ingests a repo, analyzes it, plans a change, generates code, self-reviews, and exports a patch — using Ollama locally or Gemini when deployed.

## Next 3 months — make it trustworthy enough to use on a real repo you care about

The current architecture optimizes for demo-ability (in-memory sessions, single approval gate, one-shot generation). The next phase is about closing the gap between "impressive demo" and "tool I'd actually run against my own code."

- **Persistent storage.** Replace the in-memory `Map` session store with a real database (Postgres via something like Prisma, or even SQLite for simplicity) so sessions survive a server restart and a user can return to an in-progress task.
- **Real test coverage.** Zero automated tests exist today. Start with the pieces most likely to silently regress: `diffEngine.js` normalization, `ingestionService.js`'s zip-bomb/path-traversal checks (these are exactly the kind of code you want a test locking in behavior for), and the plan/generation JSON-parsing retry logic in `llmClient.js`.
- **Multi-file dependency awareness in generation.** Right now each file in a plan is generated somewhat independently. A task that touches three files with shared state (e.g. a new prop threaded through a component tree) risks generating internally inconsistent changes. Worth exploring: passing already-generated files as context when generating later ones in the same plan.
- **Resolve the Gemini quota issue for good**, or add a graceful fallback (e.g. surfacing a clear "AI features unavailable" state instead of a generic error) so the deployed demo never looks broken to a first-time visitor.
- **Basic usage limits per session** (e.g. max plan-generation retries, max concurrent sessions) so the free-tier deployment can't be trivially abused.

## Next 6 months — from "runs one task at a time" to "actually useful for a real workflow"

- **Multi-step tasks.** Today's plan → generate → review loop assumes one task per session. A more realistic developer workflow is a sequence of small changes building on each other — support re-entering the loop with the previously generated code as the new baseline.
- **PR integration.** Instead of only exporting a `.patch` file, open an actual pull request against the connected GitHub repo (via the GitHub API) with the generated `CHANGES.md` as the PR description. This turns the tool from "generates something you copy elsewhere" into "generates something that lands directly in your workflow."
- **Support for a second language ecosystem.** The framework detector and analysis pipeline are JS/TS-specific by design. Python (Django/Flask/FastAPI) is a natural next target given overlap with common bootcamp/portfolio stacks.
- **Cost/latency dashboard.** Now that both Ollama and Gemini are supported, surface which provider and model handled a given generation, and roughly how long it took — useful both for your own debugging and as a credible "I thought about production concerns" talking point.

## Next 12 months — the version worth charging for or open-sourcing seriously

- **Team/org support with real auth.** Multiple users, shared repo connections, role-based approval (e.g. a senior engineer approves plans before code generation runs) — this is the point where "no auth" stops being a reasonable scope cut.
- **Fine-tuned or RAG-augmented planning.** Generic LLM planning works but occasionally over-includes loosely related files (noted as a known Day 5 model-behavior quirk). A retrieval layer over the actual repo's structure and past accepted/rejected plans could meaningfully improve plan precision over time.
- **Self-hosted deployment option.** Package the whole thing (frontend, backend, and an Ollama sidecar) as a Docker Compose setup so a team can run codeAgent entirely on their own infrastructure against a private repo — closing the "public GitHub URLs only" limitation from Day 3.
- **Plugin/extension model** for custom validation rules — e.g. a team could register their own lint/security checks that run automatically as part of the self-review step, beyond what the generic LLM self-review catches.

The throughline across all three horizons: everything here builds on the pipeline that already exists rather than replacing it. The Day 1–10 architecture (ingest → analyze → plan → approve → generate → review → export) is the right shape for this problem; the growth from here is about durability, trust, and integration — not a rewrite.
