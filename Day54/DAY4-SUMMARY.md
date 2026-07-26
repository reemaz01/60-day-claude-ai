# Day 4 Summary — Codebase Analysis Engine

## Objective
Build framework detection, a file-level dependency graph, key-file identification, and an LLM-generated architecture summary, surfaced end-to-end in a frontend analysis screen.

## What was built

| Feature | File | Status |
|---|---|---|
| Framework/library detection | `server/src/services/frameworkDetector.js` | ✅ Done |
| Import/require parsing + dependency graph | `server/src/services/dependencyGraph.js` | ✅ Done |
| Key files identification | `server/src/services/frameworkDetector.js` | ✅ Done |
| LLM-generated architecture summary | `server/src/services/architectureSummary.js` | ✅ Done |
| LLM client | `server/src/services/llmClient.js` | ✅ Done |
| Route: `POST /api/analysis/:sessionId` | `server/src/routes/analysis.js` | ✅ Done |
| Frontend: analysis screen (badges, summary, key files, dependency overview) | `client/src/...` | ✅ Done |

## Key decisions & pivots

**LLM provider changed twice.** Started with Gemini, hit a persistent 403 error tied to API key/project configuration. Switched to OpenAI, which then hit a 429 quota/billing error. Rather than spend a paid capstone budget on API credits, settled on **Ollama** (local inference) — free, no external dependency, no billing risk during grading/demo.

**Model size mattered more than expected.** Initially used `llama3.1:8b`, which technically worked but ran at ~0.13 tokens/sec on this machine (CPU-only, no GPU acceleration) — a simple test prompt took ~4 minutes, and the full architecture-summary prompt (with dependency graph + key files as context) consistently timed out even with a 2-minute timeout. Switched to `llama3.2:1b`, which runs at ~9.6 tokens/sec on the same hardware — a ~70x speedup — and comfortably generates real summaries in single-digit seconds. Quality tradeoff is acceptable: summaries are shorter and more generic than a larger model would produce, but accurate and clearly non-fallback.

**`localhost` vs `127.0.0.1`.** Hit an intermittent "Connection error" from the Node backend to Ollama even while Ollama was confirmed running. Root cause: Ollama's HTTP server binds to `127.0.0.1` specifically, and on this Windows setup `localhost` was inconsistently resolving (IPv6 `::1` vs IPv4). Fixed by hardcoding `baseURL: 'http://127.0.0.1:11434/v1'` in `llmClient.js` instead of using `localhost`.

## Final architecture

```
Frontend (React/Vite)
   → POST /api/repo/from-url (ingest repo, create session)
   → POST /api/analysis/:sessionId
        → frameworkDetector.js   (frameworks, key files)
        → dependencyGraph.js     (import graph, stats)
        → architectureSummary.js
             → llmClient.js → Ollama (llama3.2:1b) @ 127.0.0.1:11434
        → response: { detectedFrameworks, keyFiles, dependencyGraph,
                       dependencyStats, architectureSummary, notablePatterns }
```

## Verified against real test repo
Tested end-to-end against `https://github.com/reemaz01/codeAgent` (33 files) via both direct API calls and the live frontend UI. Confirmed:
- Framework badges render correctly: React, Express, Vite
- Architecture summary generates real, accurate, non-fallback text
- Key files list populates correctly
- Dependency overview shows correct file/import counts

Example generated summary:
> "A Node.js application built using React for the frontend, Express.js for the backend, and Vite as a build tool, serving a centralized repository management system with API endpoints for CRUD operations."

## Known limitations / follow-ups
- Ollama must be running locally (`ollama serve`) for the LLM summary feature to work — this is a **local-only dependency**. If Day 4+ requires a public deployed URL for grading, this will need to be revisited (either self-host a VM with Ollama, or add a cloud-provider fallback in `llmClient.js`).
- `llama3.2:1b` trades summary depth for speed; worth reassessing model choice if reviewers value more nuanced summaries over responsiveness.

## Status
Day 4 objective fully met. All blueprint checkpoints (backend logic, route, frontend rendering) verified against a real repository.
