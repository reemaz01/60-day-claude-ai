Day 27
Build a Prior Authorization Story Simulator


# Prior Authorization Story Simulator

An interactive, story-driven educational simulator that teaches patients and learners how the healthcare **Prior Authorization (PA)** process works — from a doctor's prescription all the way through insurance review, denial, appeal, and final approval.

Built as a single self-contained HTML file. No build tools, no dependencies to install, no backend required.

---

##Prior Authorization Story Simulator
open prior-auth-simulator.html
### [Commit: 0f28f08bd5cd6208b5593ca25ddc4675ec4109d6]



---

## What It Does

The simulator follows **Rahul** (a patient newly diagnosed with Rheumatoid Arthritis) and **Priya** (a healthcare operations specialist) through 8 scenes that cover the full PA lifecycle. At the end of each scene, the user chooses from 2 options that influence which variant dialogue plays at the start of the next scene — making each playthrough feel slightly different based on what the user wants to explore.

### The 8 Scenes

| # | Scene | What Happens |
|---|-------|--------------|
| 1 | **Doctor Visit** | Rahul is diagnosed with RA at City Medical Center. Dr. Patel prescribes Humira. Priya introduces the concept of Prior Authorization. |
| 2 | **Insurance Roadblock** | Dr. Patel's office submits a PA directly to StarCare Health (the payer). The PA flow is visualized: Provider → PA Request → Payer. |
| 3 | **What is PA?** | Priya explains Prior Authorization in plain language. Covers step therapy, disease progression risk, and the AMA 2023 PA Survey finding on treatment delays. |
| 4 | **Insurance Review** | StarCare Health checks four criteria: eligibility, clinical documentation, ICD-10 code match (M05.9), and step therapy history. |
| 5 | **Denial** | PA is denied — denial code `ST-MISSING` (missing step therapy documentation). Priya clarifies that a denial is not permanent and notes the 2+ staff-hour burden denials place on provider offices. |
| 6 | **Appeal** | The appeal is built: patient history, lab records, step therapy exception, Letter of Medical Necessity, and formal filing. |
| 7 | **Approval** | PA is approved. Reference number `SC-2024-RA-049812` is issued. The approval is saved on file — no repeat PA needed for Humira. |
| 8 | **Takeaways** | Two perspectives: what Rahul learned as a patient, and how health systems track denial rate, appeal rate, and resolution time. |

---

## Characters

| Character | Role | Position in Chat |
|-----------|------|-----------------|
| 👦 **Rahul** | Patient — newly diagnosed with Rheumatoid Arthritis | Left (indigo bubbles) |
| 👧 **Priya** | Healthcare Operations Specialist | Right (teal bubbles) |
| *Narrator / Dr. Patel* | Scene-setting context | Centered italic text — never chat bubbles |

> StarCare Health is used as an **illustrative example** throughout and does not represent any real insurance provider.

---

## Technical Details

### Stack

- **HTML5** — single file, no bundler or build step
- **Tailwind CSS** — loaded via CDN (`cdn.tailwindcss.com`)
- **Google Fonts** — Inter (400, 500, 600, 700), loaded via CDN
- **Vanilla JavaScript** — no frameworks, no npm packages

### Architecture

```
prior-auth-simulator.html
├── <style>          CSS custom classes + animations (Tailwind can't cover everything)
├── HTML layout      Header, #chat-feed, #choices-area
└── <script>
    ├── SCENES[]     Data layer — all 8 scenes, messages, variants, choices
    ├── Renderers    createElement-based builders for each message type
    ├── enqueueMessages()   Sequential animation queue with per-type delays
    ├── renderChoices()     Choice buttons + restart logic
    └── startScene()        Scene orchestrator — merges variant + main messages
```

### DOM Safety Rule

**`innerHTML =` is never called on the chat container.**

Every chat bubble, narrator line, card, and diagram is built using `createElement` and `appendChild` only. This prevents XSS injection from content data and keeps the feed strictly append-only throughout the session.

### Message Types

Each message in the `SCENES` data array has a `type` field. The `buildElement()` function dispatches to the correct renderer:

| `type` | Renderer | Renders As |
|--------|----------|------------|
| `rahul` | `createBubble('rahul', ...)` | Left-aligned chat bubble (indigo) |
| `priya` | `createBubble('priya', ...)` | Right-aligned chat bubble (teal) |
| `narrator` | `createNarrator(...)` | Centered italic text |
| `flow` | `createFlowDiagram(...)` | Horizontal flow diagram with arrow connectors |
| `checklist` | `createChecklist(...)` | Icon + label + description list card |
| `steps` | `createSteps(...)` | Numbered step cards with gradient number badges |
| `stat` | `createStat(...)` | Highlighted stat/citation card |
| `denial` | `createDenial(...)` | Red-bordered denial banner with denial code |
| `approval` | `createApproval(...)` | Green-bordered approval banner |
| `refnum` | `createRefNum(...)` | Monospace PA reference number chip |
| `takeaway-header` | `createTakeawayHeader(...)` | Bold teal section divider |
| `metrics` | `createMetrics(...)` | Left-bordered metric cards (one per KPI) |

### Scene Branching (Variants)

Each scene can have a `variants` object keyed by variant ID (e.g., `"2a"`, `"2b"`). When a user selects a choice, its `next` value is passed as `variantKey` to the next scene's `startScene()` call.

```js
// Scene 2 example
variants: {
  "2a": [ { type: "rahul", text: "Why can't I just pick up my prescription right now?" }, ... ],
  "2b": [ { type: "rahul", text: "How long does this PA process usually take?" }, ... ]
}
```

The variant messages are prepended before the scene's shared `messages` array, so the scene always resolves to the same core content regardless of which choice was made.

### Animation Timing

Messages are revealed sequentially via `enqueueMessages()`. Delays vary by type to feel natural:

| Message type | Delay before next |
|---|---|
| `narrator`, `takeaway-header` | 300ms |
| `rahul`, `priya` (chat bubbles) | 750ms |
| All other rich content | 500ms |

Each element also has a CSS `bubbleIn` keyframe animation (opacity + translateY) on entry.

### Progress Bar

The header progress bar advances automatically on `startScene()`:

```js
document.getElementById('progress-bar-fill').style.width = (sceneId / 8 * 100) + '%';
```

Transitions at `0.6s cubic-bezier(0.4, 0, 0.2, 1)`.

---

## Design System

### Color Palette

| Role | Hex | Usage |
|------|-----|-------|
| Background | `#0F2442` | Page background |
| Surface dark | `#0A1929` | Header, choices footer |
| Teal accent | `#0D9488` | Priya bubbles, progress bar, choice borders, flow arrows |
| Indigo accent | `#6366F1` | Rahul bubble borders (via rgba) |
| Denial red | `#EF4444` | Denial banner, metric border |
| Approval green | `#10B981` | Approval banner, reference number chip |
| Warning amber | `#F59E0B` | Appeal rate metric border |
| Text primary | `#E2E8F0` | Bubble body text |
| Text muted | `#94A3B8` | Narrator text, labels |

### Typography

- **Font:** Inter (Google Fonts)
- **Weights used:** 400 (body), 500 (labels), 600 (sub-headings), 700 (titles)
- **Monospace:** System monospace stack — used for PA reference numbers only

---

## Customization

### Adding a New Scene

1. Append a new object to the `SCENES` array in the `<script>` block.
2. Set `id` to the next integer, `label` to a short scene name.
3. Add `messages` (array of message objects) and `choices` (array of `{ label, next }` objects).
4. Optionally add `variants` keyed to the `next` values from the previous scene's choices.
5. Set `final: true` on the last scene to show the Restart button instead of choices.

### Adding a New Message Type

1. Write a `createXxx(...)` function that returns a DOM element.
2. Add a `case 'xxx':` entry in `buildElement()`.
3. Use the new `type` value in any scene's `messages` array.

### Changing Animation Delays

Edit the delay values in `enqueueMessages()`:

```js
const delay = msg.type === 'narrator' ? 300
  : msg.type === 'rahul' || msg.type === 'priya' ? 750
  : 500;
```

---

## Educational References

- **AMA 2023 Prior Authorization Physician Survey** — cited in Scene 3. Source: American Medical Association.
- **MGMA Provider Research** — PA denial resolution time (2+ staff hours). Cited in Scene 5.
- **ICD-10 Code M05.9** — Rheumatoid arthritis, unspecified. Used in Scenes 2 and 4.
- **Humira (adalimumab)** — biologic DMARD, used as a real-world example medication throughout.
- All insurer references use **StarCare Health** as a fictional illustrative example.

---

## License

This project is for educational purposes. Healthcare information is illustrative and not intended as medical or legal advice.
