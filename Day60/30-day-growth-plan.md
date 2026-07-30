# 30-Day Growth Plan — Post-codeAgent

*What comes next after the 60-Day Claude AI Mastery Challenge*

---

## Why this plan exists

codeAgent proved I can ship a full AI agent pipeline end-to-end: ingest, analyze, plan, generate, review, export, with real security hardening and a server-enforced approval gate — not a toy demo. The next 30 days are about converting that into (a) a more defensible, production-grade version of the project, and (b) a stronger interview-ready profile for SWE/full-stack + AI/ML internships.

This plan is organized in three parallel tracks, worked in short daily blocks rather than one big push.

---

## Track 1: Harden & extend codeAgent (Days 1–15)

**Week 1 — Fix what recruiters will notice first**
- Resolve the Gemini quota issue so the live demo reliably works end-to-end (add graceful fallback/error handling if a provider is rate-limited, or add a request-queue/backoff)
- Finish the diff viewer / self-review step that was backlogged from Day 7
- Reconcile the "Step X of 9" UI copy with the real 7-step flow, and add a one-line onboarding description above the repo input

**Week 2 — Depth over breadth**
- Add automated tests for the security-hardening paths (path traversal, zip-bomb, CORS) so they're provably covered, not just claimed
- Add a second LLM provider integration test / fallback path to make the "dual-provider abstraction" claim demonstrable in a live run
- Record a 2–3 minute demo video/GIF for the README

## Track 2: Portfolio & interview readiness (Days 10–22, overlapping)

- Finalize resume bullets and a one-paragraph project pitch (functionality, architecture, engineering decisions, outcome)
- Prepare answers for the likely interview questions: "walk me through the architecture," "what was the hardest bug," "what would you do differently," "how does the approval gate work and why does it matter"
- Publish a build-in-public recap post on LinkedIn summarizing the 60-day challenge, tagged appropriately, linking the live demo and repo
- Update GitHub profile README and pin codeAgent alongside Musefolio

## Track 3: Skill-building beyond the challenge (Days 15–30)

- Pick one gap surfaced during the challenge (e.g., testing discipline, deployment/CI, or agent-orchestration patterns) and go one level deeper with a focused mini-project or course module
- Apply to a rolling batch of SWE/full-stack and AI/ML internships, using codeAgent and Musefolio as the two flagship links
- Do 2–3 mock interviews (technical + behavioral) referencing codeAgent as the primary project to talk through

---

## Weekly checkpoints

| Week | Primary goal | Done when |
|---|---|---|
| 1 | Demo reliably works, UI copy fixed | Live app usable end-to-end without errors |
| 2 | Tests + provider fallback in place | CI green, second provider path demonstrable |
| 3 | Portfolio content finalized | Resume, pitch, recap post published |
| 4 | Applications + interview prep | X applications sent, 2+ mock interviews done |

---

## Guardrail

The point of this plan is momentum without burnout — short daily blocks, not another 10-day sprint. If a week slips, cut Track 3 first, protect Track 1 and 2.
