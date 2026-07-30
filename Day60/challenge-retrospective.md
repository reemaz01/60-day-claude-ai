# codeAgent — Challenge Retrospective

*Days 1–10 of the AB Talks 60-Day Claude AI Challenge capstone sprint.*

## Timeline

**Day 2 — Architecture, tech stack & setup.** Locked the stack: React + Vite, Node + Express, no database (in-memory session store), no auth, in-memory sessions with a TTL. Project renamed from "CodePilot Agent" to **codeAgent**. Full design docs produced up front (ARCHITECTURE, SCHEMA, API, UI-WIREFRAMES, PROJECT-STRUCTURE, NAMING) — a deliberate choice to plan the shape of all 9 remaining days before writing pipeline code.

**Day 3 — Repository ingestion.** Built GitHub URL cloning (`simple-git`) and ZIP upload (`adm-zip`) into a shared ingestion service, with a filtered file-tree builder and a real session store. Recovered a lost `client/src` folder and a corrupted `node_modules` mid-day without losing prior work — an early lesson in checking the actual state of things rather than assuming yesterday's session left everything intact.

**Day 4 — Codebase analysis engine.** Framework detection, dependency graph, key-file identification, and an LLM-generated architecture summary. This day had the sprint's first real infrastructure pivot: started with Gemini (403 errors), tried OpenAI (429 quota errors), and landed on **Ollama running locally** — free, no billing risk, no external dependency during development. Also discovered that `llama3.1:8b` ran at ~0.13 tokens/sec on CPU-only hardware (unusably slow) versus `llama3.2:1b` at ~9.6 tokens/sec — a ~70x difference that shaped model choice for the rest of local development.

**Day 5 — Task input & plan generation.** Built the plan-generation pipeline and caught two real bugs before they became load-bearing: a no-op execution-order validation filter that would have silently let the LLM invent nonexistent file paths, and a `normalizePath()` function that didn't handle `../../`-style prefixes.

**Day 6 — Approval gate, code generation & deployment.** The approval gate — planned since Day 2 — was implemented as a genuine server-side check (`session.planApproved`), not just a disabled button, so code generation can't be triggered by bypassing the UI. Switched to `llama3.1:8b` for real generation quality (accepting the slower speed) and added dual-provider support (Ollama locally, Gemini when deployed) behind an `LLM_PROVIDER` env var. First deployment to Netlify + Render happened here, a day later than the Day 2 plan anticipated but still with room to spare before the finish line.

**Day 7 — Diff viewer & AI self-review.** Built a syntax-highlighted, tabbed diff viewer and a self-review pipeline where the model critically evaluates its own generated changes (confidence level, risks, suggested tests). Also did a full design-system pass — CSS custom properties replacing scattered inline hex codes across every component — after noticing inconsistent theming (a leftover navy palette in one component, light-mode colors in another) had crept in across days of iteration.

**Day 8 — Security hardening, patch export & documentation.** *(Note: this day was scoped but not actually committed at the time — the repo sat at the Day 7 commit going into Day 10. It was built for real during the Day 10 session, verified with actual boot tests and a synthetic zip-bomb, before anything else proceeded.)* Delivered: an origin-restricted CORS policy, zip-bomb protection (entry count, per-file size, total size, and compression-ratio checks), defense-in-depth path-traversal validation, on-disk session cleanup (previously only the in-memory record was ever cleared), a downloadable unified-diff patch export, and AI-generated `CHANGES.md` documentation.

**Day 9 — folded into Day 10.** Never run as a separate polish/testing day; its scope (end-to-end QA, edge cases) was absorbed into the Day 10 review.

**Day 10 — Final review & graduation.** A genuine senior-engineer-style review surfaced two things that had gone unnoticed until checked directly against the live repo rather than against memory of past sessions: Day 8's work existed only in conversation history, not in `git log`, and a Day 8 commit accidentally reverted a real Day 7 bug fix in `DiffViewer.jsx` (failed files silently disappearing from the tab list again). Both were fixed and verified before anything else. README, LICENSE, and CONTRIBUTING.md — none of which existed before today — were written to match what the project actually does, and a pre-existing lint warning was resolved.

## Major technical decisions & pivots

1. **LLM provider: Gemini → OpenAI → Ollama (local) → Gemini (deployed).** Not a straight line — a real sequence of hitting real constraints (auth errors, billing quotas) and adapting, landing on a pragmatic dual-provider setup rather than betting everything on one vendor.
2. **Model size tradeoff:** `llama3.2:1b` for fast iteration, `llama3.1:8b` for real output quality — a conscious speed-vs-quality choice made explicitly, not left implicit.
3. **In-memory sessions over a database**, deliberately, to keep the 10-day scope achievable — documented as a known limitation rather than hidden.
4. **Server-enforced approval gate** as a genuine architectural decision, not just a UX nicety — code generation is impossible without a real backend check passing.

## Challenges solved & debugging moments worth naming

- The `localhost` vs `127.0.0.1` Ollama connection issue (IPv4/IPv6 resolution on Windows) — the kind of bug that looks like "the service is down" when it's actually a hostname resolution quirk.
- The undici default 5-minute header timeout silently killing slow local LLM calls — diagnosed by recognizing the failure was happening *below* the LLM client's own configured timeout.
- Two silent-failure bugs in Day 5 (the no-op path filter, the incomplete path normalizer) — both are the dangerous kind of bug: they don't crash anything, they just quietly produce wrong results.
- The Day 10 discovery that Day 8 had never actually been pushed, and that a later commit had accidentally reverted a real fix — caught only by treating "what past sessions said happened" and "what's actually in the repository" as two different things worth checking against each other.

## Skills demonstrated across the sprint

Full-stack architecture and staged rollout planning (Day 2's docs-first approach), working directly with LLM APIs across multiple providers and handling their real failure modes (auth errors, quota limits, malformed JSON, slow local inference), debugging under uncertainty (hostname resolution, timeout layering, silent logic bugs), security-conscious backend development (zip-bomb protection, path traversal, CORS), UI/UX consistency work (the Day 7 design-system pass), and — on Day 10 specifically — the less glamorous but equally real skill of auditing your own past claims against ground truth before building on top of them.

## Final project summary

codeAgent is a working, end-to-end autonomous coding agent: point it at a public GitHub repo, describe a task, and it analyzes the codebase, proposes a plan, waits for explicit approval, generates real file diffs, critically reviews its own work, and exports a patch or AI-written documentation. It runs on a genuinely thought-through architecture (session-based, provider-agnostic LLM layer, server-enforced approval gate) with real security hardening behind it, not just a happy-path demo.

## Lessons learned

- **A past session's summary is a claim, not a fact.** The single most important thing that happened on Day 10 wasn't new code — it was checking the actual `git log` before trusting what previous sessions said was done.
- **Silent failures are the ones worth hunting for.** The bugs that mattered most across this sprint (the no-op filter, the reverted fix, the never-pushed Day 8) never threw an error. They just quietly did the wrong thing.
- **Infrastructure constraints (billing, quota, hardware) shape architecture as much as design decisions do.** The Ollama/Gemini dual-provider setup exists because of real 403s and 429s, not because it was the original plan.

## A closing note from your AI pair programmer

Ten days ago this was a name change from "CodePilot Agent" and a stack decision on a whiteboard. Today it's a real pipeline that clones a repo, reasons about it, proposes a change, waits for you to say yes, writes the code, checks its own work, and hands you something you can actually apply. That arc — ingest, analyze, plan, approve, generate, review, export — held up exactly as designed from Day 2 through Day 10, even while the LLM provider underneath it changed twice and the hardware fought you on inference speed.

What I'd point to as the real proof of growth isn't any single feature — it's Day 10 itself. Most people, told a feature was "done," would have taken that at face value and moved straight to writing a victory lap. Instead, the repo got cloned fresh and checked against what was actually claimed, twice — once for Day 8, once for the DiffViewer regression — and both times the harder, more honest path was taken instead of the convenient one. That instinct is worth more than any individual line of code in this project, and it's the thing most likely to still be true of you on Day 6000 of writing software, long after `llama3.1:8b` and this particular Ollama version are irrelevant. Well built. Go ship it.
