# learn-any-ai-project

A **generic AI-project learning engine** — a single self-contained Agent skill that teaches you *any* mainstream AI project (RAG / Agent / LLM apps / CV / speech / multimodal / AIGC / recommender / classic ML & NLP / LLM fine-tuning / AI data engineering / model serving & AI platforms / AI testing & evaluation) from scratch, without binding to any specific project.

> **中文版说明见 [README.zh-CN.md](./README.zh-CN.md)**

**The core idea in one sentence**: instead of dumping a fixed course outline, the skill derives a chapter-based learning plan (**LEARN.md**) from *first principles* — the chapter count, topics and order are decided by the target project's own profile, never by a template. Learning is driven through a review gate, per-chapter generation with local green-check verification, a `.engine/state.json` ledger for two-way doc↔artifact state sync, and hands-on practice that ends in a blind rehearsal — **"learned" means *you* can run it, not that the Agent ran it**.

---

## Why this skill exists

Most "learn AI project X" tutorials are textbooks for one project. If the project is different — different type, different stack, different stage — the chapters don't fit. This skill is a *methodology engine*: it asks "which closed loops (rings) must you walk through to truly understand *this* system?", folds those rings into chapters, and renders a handbook whose structure matches the actual project. The skill carries **zero project content**: no paths, no file names, no tool stacks, no trademarks — safe to copy into any repo and safe to share on GitHub.

## Key features

| Feature | What it means |
|---|---|
| **Zero project dependency** | No references to any concrete project; works for open-source and closed-source targets alike |
| **First-principles chapter derivation** | Chapter count / topics / order come from the project profile, not from templates (anti-copy check included) |
| **Covers mainstream AI types** | A layered index (§5.3) hints at distinguishing rings for 15+ types; unmatched/new shapes still work — the method never depends on matching the table |
| **Review gate** | A hard human checkpoint before any code is written — you approve the plan first |
| **State ledger & two-way sync** | `.engine/state.json` is the single source of truth; doc status cards are projections; sha256 drift auto-detects `verified → dirty` |
| **Hands-on-first learning** | Every chapter embeds hands-on points (X.6); services/deps/commands are executed by *you*, the Agent only explains and verifies; a closing **blind rehearsal** proves independent delivery |
| **Lean output discipline** | Minimal sufficient code, artifact cleanliness (temp files cleaned), no "XX version" labels, no filler — the produced docs/code are shippable assets |
| **Language follows the user** | Conversation and all artifacts are written in your current language (Chinese / English / …) — nothing hardcoded; proper nouns and commands stay untranslated |
| **Bilingual spec** | `SKILL.md` (Chinese, authoritative) + `SKILL.en.md` (English, 1:1 translation), bound by a terminology contract in `docs/terminology.md` |

## Repository layout

```
learn-any-ai-project/
├── README.md                        # This overview (English)
├── README.zh-CN.md                  # 中文总览
├── LICENSE                          # MIT License
├── .gitignore                       # Runtime ledgers / env / caches / drafts
├── docs/
│   └── terminology.md               # 中英术语对照表 — translation contract between the two SKILL versions
└── skills/
    └── learn-any-ai-project/
        ├── SKILL.md                 # The skill spec — Chinese (authoritative)
        └── SKILL.en.md              # The skill spec — English (1:1 translation)
```

## Quick start

### Option A (recommended) — install with one prompt

In your AI Agent's chat (any agent with web access and file-writing), paste the prompt below. The Agent downloads and installs the skill for you — no manual file copying:

```
Please install the "learn-any-ai-project" skill:
1. Download it from https://github.com/Yuanqs-pine/learn-any-ai-project — take SKILL.md (Chinese) or SKILL.en.md (English) under skills/learn-any-ai-project/.
2. Save it to your agent's skill directory, e.g. ~/.workbuddy/skills/learn-any-ai-project/SKILL.md (adjust to your agent's location).
3. Reload the skill, then reply "learn-any-ai-project installed".
```

> If your Agent has a skill marketplace / installer, you can also search for "learn-any-ai-project" and install it in one click.

### Option B — install manually

Copy `skills/learn-any-ai-project/SKILL.md` (Chinese) or `SKILL.en.md` (English) into your agent's skill directory (e.g. `~/.workbuddy/skills/learn-any-ai-project/SKILL.md`), then reload the agent. Both files are self-contained single files — no extra scripts, no bundled assets.

### After installing — how to use it, step by step

1. Open a chat in the project directory you want to learn, and say a trigger phrase: *"Learn this project systematically"* (also works: "generate a learning plan for this project", "build learning docs in handbook style").
2. The skill runs **S0 Profile** — it probes the project and asks a few questions (type / scale / stack / stage / goal / environment constraints / sharing / language). Answer them.
3. It derives a chapter map from first principles and renders **LEARN.md** in the project root.
4. **Review gate**: read LEARN.md and confirm before any code is written — adjust chapters if they don't fit.
5. Then chapter by chapter (S3 → S4 → S5):
   - **Environment first** — you install deps and start daemon/GUI services yourself (the Agent never auto-launches them).
   - **Each chapter** — the Agent explains and generates, runs a local green check, then hands you "hands-on points" to execute yourself; finally it syncs state to the ledger.
   - **Each chapter close** — you do an oral recap (three questions) in the chat.
6. **Blind rehearsal** at the end: with all commands hidden, run the minimal chain end-to-end yourself. Pass it and you have genuinely learned the project.

### What the skill creates at runtime

| Item | Where | Purpose |
|---|---|---|
| `LEARN.md` | target project root | The chapter-based handbook (layout per §6 of the skill) |
| `.engine/state.json` | target project root | Auto-created runtime ledger — single source of truth for chapter/artifact status; never shipped by the skill itself |

Nothing else. No teaching junk, no temp files left behind.

## How it works (S0–S5 pipeline)

```
S0 Profile ──► S1 Derive rings ──► S2 Render LEARN.md ──► [Review gate] ──► S3 Environment
                                                                    │
                              S5 Closing acceptance ◄── S4 Per-chapter loop (align → generate
                              (+ blind rehearsal)         → verify → sync → close)
```

- **S0 Profile**: probe + ask 9 dimensions (type / scale / stack / stage / goal / delivery form / env constraints / sharing / language).
- **S1 Derive**: 7-question checklist finds the rings; folding rules turn rings into chapters; §5.3 layered index gives hints per project type; anti-copy check keeps it honest.
- **S2 Render**: LEARN.md follows a fixed *shape* (document header with profile + progress table + reading guide, uniform chapter skeleton X.1–X.6) but free *content*.
- **Review gate**: 7 criteria, all must pass — user confirmation is mandatory before any code.
- **S3 Environment**: highest hands-on chapter — you install deps and start services; the Agent verifies minimal connectivity.
- **S4 Loop**: align → generate/explain → **dual-track verify** (Agent green check + your hands-on run must match) → sync to ledger → oral recap.
- **S5 Acceptance**: closing acceptance + blind rehearsal + artifact-cleanliness re-check.

## Supported project types (§5.3 index)

| Layer | Types |
|---|---|
| Application | LLM text apps, RAG knowledge-base QA, Agents, CV apps, speech apps, multimodal apps, AIGC generative tools, recommender systems |
| Model | Classic ML & NLP pipelines, LLM fine-tuning & alignment, AI data engineering |
| Platform | Model inference/serving platforms, AI gateways & observability, low-code AI app platforms |
| Quality | AI testing & evaluation engineering (cross-cutting) |

Types not listed (including brand-new shapes) run the same derivation flow — **the method's validity never depends on matching the table**. Open-source and closed-source targets are both supported (white-box adds source-reading rings; black-box swaps them for doc/API/probing rings).

## Design principles (details in SKILL §1)

Zero project dependency · custom content / uniform form · first principles · single source of truth (ledger) · lightweight & self-contained · learning produces deliverables · hands-on first (practice ≥ demo) · zero "versions" & zero filler · lean & clean deliverables · language follows the user.

## Terminology contract

`SKILL.md` and `SKILL.en.md` are kept 1:1 in sync under the translation contract in [docs/terminology.md](./docs/terminology.md) — one Chinese concept maps to exactly one fixed English term. When you extend the skill, update the Chinese spec, then mirror it in English using the contract table.

## License

[MIT](./LICENSE) © 2026 Lilpinecone
