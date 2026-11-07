# Shaping AI Coding Agents with Skills: From Local Prototype to Production on Google Cloud

**Google Antigravity (`agy`) & Agent Skills (`SKILL.md`): Baseline Vibe-Coding, Disciplined Local Architecture (`mattpocock/skills`), and Low-Cost Serverless Production (`google/skills`)**

A live-recorded two-run experiment (with a Stage 3 Google Cloud productionization walkthrough), interactive `/teach-code` **Codelabs** ([`./codelab/`](./codelab/)), and Slidev presentation deck ([`./slides/`](./slides/)) demonstrating how always-on Rules (`AGENTS.md`) and composable Agent Skills (`SKILL.md`) reshape how Google Antigravity (`agy`) designs, builds, and productionizes an audio electronics **Component** and **Kit** inventory web system.

> **Core Thesis**: *"Without skills, an AI coding agent will happily one-shot a local web prototype while burying domain rules and architectural trade-offs in ephemeral chat history. By composing engineering workflow skills (`mattpocock/skills`) with cloud architecture and deployment skills (`google/skills`), you turn `agy` into a disciplined engineering partner—building a tested Rust + HTMX + Turso/libSQL web application behind a clean repository seam, ready to swap persistence to **Cloud Firestore** and deploy scale-to-zero on **Cloud Run** (`$0/month` idle within the free tier)."*

---

## Agent Skill Repositories Used

Installable into `.agents/skills/` across Google Antigravity (`agy`), Claude Code, Cursor, and other harnesses via `npx skills`:

- **[`mattpocock/skills`](https://github.com/mattpocock/skills)** — Run 2 (**Skilled Run**) Engineering Workflow & Domain Modeling Skills (`/wayfinder`, `/grilling`, `/domain-modeling`, `/research`, `/prototype`, `/tdd`, `/code-review`, `/to-spec`, `/to-tickets`, `/implement`):

  ```bash
  npx skills@latest add mattpocock/skills
  ```

- **[`google/skills`](https://github.com/google/skills)** — Stage 3 (**Production Run**) Google Cloud Architecture, Database Onboarding, Cost Optimization & Deployment Skills (`cloud-run-basics`, `cloud-databases-onboarding`, `google-cloud-waf-cost-optimization`, `gcloud`, `firebase-firestore`, `firestore-rules-creation`):

  ```bash
  npx skills@latest add google/skills
  ```

- **[`domesticmouse/skills`](https://github.com/domesticmouse/skills)** — Interactive Codelab, Recording & Presentation Reproducibility Skills (`/teach-code`, `/slidev-deck`, `/asciinema`, `/cast-player-html`, `/agy-brain-explorer`):

  ```bash
  npx skills@latest add domesticmouse/skills
  ```

---

## The Controlled Two-Run Experiment & Production Stage

Runs 1 and 2 are live-recorded terminal sessions starting from the **exact same initial prompt** (with no mention of Google Cloud) and answering clarifying questions from the same **Canonical Q&A** in [`RECORDING_RUNBOOK.md`](./RECORDING_RUNBOOK.md):

> `"I'd like to build a web application to track my audio electronics components inventory and DIY kit builds."`

1. **Run 1 — Baseline Run (`01-baseline.cast`, `audio_inventory_baseline`)**:
   - **Setup**: Empty directory, guided only by the user's global one-question-at-a-time rule (`$HOME/.gemini/config/AGENTS.md`) with **no** repository skills installed.
   - **Outcome**: `agy` interviews the operator one question at a time and builds a working local web application using its default local stack (Python + FastAPI + SQLite), seeded with audio electronics **Components** (`SMT` and `THT` parts like `TL074`, `NE5532`, `LM13700`) and DIY **Kits**, followed by `/clear` → `Please review the codebase` → `please fix`. Domain vocabulary and architectural decisions remain locked in chat transcripts rather than durable repository artifacts.

2. **Run 2 — Skilled Run (`02-skilled.cast`, `audio_inventory_skilled`)**:
   - **Setup**: Fresh directory with [`mattpocock/skills`](https://github.com/mattpocock/skills) installed (`npx skills@latest add mattpocock/skills`).
   - **Outcome**: Driven via `/wayfinder` → `/to-spec` → `/to-tickets` → `/implement` (with `/clear` between sessions), `agy` models the domain in `GLOSSARY.md` and `docs/adr/`, prototypes UI variants, slices vertical tickets, and builds a tested **Rust (Axum + Maud) + HTMX + local Turso (`libSQL`)** workbench web application with 41 integration tests behind a clean repository module seam (`src/db.rs`).

3. **Stage 3 — Production Run (Architectural Codelab & Slidev Walkthrough)**:
   - **Setup**: Presented as an architectural walkthrough and interactive capstone exercise (without a live terminal recording), starting from the completed **Skilled Run** workspace (`audio_inventory_skilled`) augmented with [`google/skills`](https://github.com/google/skills) (`npx skills@latest add google/skills`).
   - **Prompt**:
     ```text
     /wayfinder I'd like to adapt and productionize this web application for a low-volume, low-cost deployment on Google Cloud using Cloud Run and Cloud Firestore.
     ```
   - **Outcome**: Composes `mattpocock/skills` process skills with `google/skills` domain guardrails (`cloud-databases-onboarding`, `google-cloud-waf-cost-optimization`, `cloud-run-basics`, `gcloud`, `firestore-rules-creation`) to introduce an `InventoryRepository` trait seam (ADR 0002), preserve all 41 offline `TursoRepository` tests, add `FirestoreRepository` for **Cloud Firestore** (Native Mode), and deploy scale-to-zero on **Cloud Run** (`--min-instances=0`) at `$0/month` idle within the free tier.

---

## Recording & Post-Processing Workflow

See [`RECORDING_RUNBOOK.md`](./RECORDING_RUNBOOK.md) for the complete pre-flight checklist, **Canonical Q&A** copy/paste table, and step-by-step operator commands for the two recorded runs.

```bash
# Check current state of workspaces, Terminal Casts, Session Traces, and HTML cast players
./scripts/setup-workspaces.sh status

# Process each recorded run immediately after exiting asciinema rec
./scripts/setup-workspaces.sh process-run 01-baseline.cast audio_inventory_baseline
./scripts/setup-workspaces.sh process-run 02-skilled.cast audio_inventory_skilled

# Sync completed app workspaces from ~/Demos/audio-inventory-experiment into ./experiments/
./scripts/setup-workspaces.sh sync-experiments
```

---

## Wayfinder Map & Issue Tracker

Planning and execution across this repository are tracked in GitHub Issues (`domesticmouse/antigravity-cloud-presentation`):

- **Wayfinder Map**: [Antigravity Cloud Website Experiment, Codelabs, and Slidev Presentation (#1)](https://github.com/domesticmouse/antigravity-cloud-presentation/issues/1)
- To resume working through the map in a new `agy` session:
  ```text
  /wayfinder #1
  ```

---

## Repository Structure

| Path | Description |
| :--- | :--- |
| [`GLOSSARY.md`](./GLOSSARY.md) | Ubiquitous domain language (**Baseline Run**, **Skilled Run**, **Production Run**, **Terminal Cast**, **Session Trace**, **Canonical Q&A**, **Codelab**, **Component**, **Kit**). |
| [`RECORDING_RUNBOOK.md`](./RECORDING_RUNBOOK.md) | Step-by-step operator runbook for recording the `asciinema` **Terminal Casts**, injecting stop points, exporting **Session Traces**, and syncing workspaces. |
| [`scripts/setup-workspaces.sh`](./scripts/setup-workspaces.sh) | Helper CLI (`process-run`, `postprocess-casts`, `extract-traces`, `sync-experiments`, `status`) automating cast sanitization, chapter marking, HTML player embedding, and trace extraction. |
| [`scripts/markers/`](./scripts/markers/) | Canonical chapter stop-point JSON specifications ([`01-baseline.json`](./scripts/markers/01-baseline.json), [`02-skilled.json`](./scripts/markers/02-skilled.json)) used by `mark-cast.py`. |
| [`prototypes/`](./prototypes/) | Standalone 16:9 Slidev `cast-full` HTML test-drive harnesses ([`01-baseline-cast-player.html`](./prototypes/01-baseline-cast-player.html), [`02-skilled-cast-player.html`](./prototypes/02-skilled-cast-player.html)). |
| [`recordings/`](./recordings/) | Captured raw (`recordings/raw/`) and sanitized, chapter-marked, exit-trimmed (`recordings/final/`) **Terminal Casts** for the two recorded runs (`01-baseline.cast`, `02-skilled.cast`). |
| [`artifacts/traces/`](./artifacts/traces/) | Exported per-session Antigravity Markdown **Session Traces** across both recorded runs (`audio_inventory_baseline`, `audio_inventory_skilled`). |
| [`experiments/`](./experiments/) | Synced application workspaces from both recorded runs (`audio_inventory_baseline`, `audio_inventory_skilled`). |
| [`codelab/`](./codelab/) | Interactive `/teach-code` **Codelabs** (`index.md`, 5 lessons in `lessons/`, 3 printable reference sheets in `reference/`, and `build.py`) exploring when to vibe-code vs. when to engineer with skills. |
| [`slides/`](./slides/) | 5-act Slidev presentation deck walking audiences through the two recorded experiment runs, the Google Cloud productionization architecture, and the interactive **Codelabs**. |
| [`.agents/skills/`](./.agents/skills/) | Installed Agent Skills from `mattpocock/skills`, `google/skills`, and `domesticmouse/skills`. |
| [`docs/agents/`](./docs/agents/) | Agent configuration docs for GitHub issue tracking ([`issue-tracker.md`](./docs/agents/issue-tracker.md)), triage labels ([`triage-labels.md`](./docs/agents/triage-labels.md)), and domain documentation ([`domain.md`](./docs/agents/domain.md)). |

---

## License

Licensed under the [Apache License, Version 2.0](./LICENSE).

---

*This is not an officially supported Google product.*
