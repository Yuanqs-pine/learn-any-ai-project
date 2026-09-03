---
name: learn-any-ai-project
description: A generic AI-project learning skill — systematic from-scratch learning for any mainstream AI project (LLM text apps / RAG / Agent / CV apps / speech apps / multimodal apps / AIGC generative tools / recommender systems / classic ML & NLP / LLM fine-tuning & alignment / AI data engineering / model serving & AI platform infrastructure / AI testing & evaluation; layered index in §5.3). Bound to no concrete project: no references, no examples, no imports. Self-contained single file, portable across repos, safe to share on GitHub. Core capabilities: ① derive a chapter-based learning plan (LEARN.md) from first principles and the project's own profile — chapter count and topics are decided by the project itself (layout follows the built-in spec; content is never template-copied); ② progress through "user review → per-chapter alignment → generation → local green-check verification → state sync"; ③ keep `.engine/state.json` as the single source of truth for two-way state sync between docs and artifacts; ④ embed a "hands-on first" practice rule — skill-building actions are handed to the user to perform by hand; ⑤ zero-redundancy red line: no "XX version" labels, each fact written once, parentheses only for key notes, no filler; ⑥ language follows the user: the learning conversation and all artifacts (LEARN.md / docs / code comments) are written in the user's current language by default — no single language is hardcoded; proper nouns and commands stay untranslated. Triggers: learn project X, generate a learning plan for a project, build learning docs in handbook style, keep docs and code state in sync.
---

# Generic AI Project Learning Skill

Turn "systematically learning a new AI project" into a reusable pipeline: **profile → derive chapters → render the plan document → user review → per-chapter learning → two-way state sync**. This skill is a *methodology engine*, not a textbook for any project. Every project's knowledge and code are anchored in the actual files inside that project directory; the skill itself carries no project content.

## 1. Core Design Principles (why it is generic and shareable)

| Principle | Meaning |
|---|---|
| Zero project dependency | The skill contains no concrete project (no paths / file names / tool stacks / trademarks). It holds for any project and any learner |
| Custom content, uniform form | Only the "document shape and writing rules" are locked. **Chapter count, topics and order are derived from the project profile** — chapters from other projects are never reused |
| First principles | Do not guess chapters from "common templates". First ask "which closed loops (rings) must be walked through to understand this system", then derive chapters from the rings |
| Single source of truth for state | `.engine/state.json` under the target project root is the only ledger; status cards and the progress table in the doc are merely projections of it |
| Lightweight & self-contained | All mechanics (layout spec + ledger + sync rules) are defined in this file. No extra runtime scripts — the Agent executes the rules directly |
| Learning produces deliverables | What you produce while learning (code / environment / docs) stays inside the target project as shippable assets; no "teaching junk" floats outside the learning area |
| Hands-on first; practice ≥ demo | The goal is the learner's ability to deliver independently: any skill-building action (starting services / installing deps / running commands / reading logs / debugging / reproducing) is handed to the user first. The Agent explains, gives exact commands, self-verifies with green checks and acts as fallback — it never takes over "because automation is faster" |
| Zero "versions", zero filler | Generated docs / files / code are written once and are plain-language by default: no "XX version" labels (e.g. "plain-language version / formal version"); parentheses only for key notes (why / trade-offs / analogies / how to read results); delete all filler and redundancy |
| Lean & clean deliverables | Deliverables (docs / code / environment) keep only what is necessary: docs highlight key points, cuttable and reusable (§12.2-8); code minimal but sufficient (§12.1); temp / intermediate / debug files are cleaned right after use and never enter the ledger or the docs (§9.1) |
| Language follows the user | The skill presets no language: the language of the learning conversation and of all artifacts (LEARN.md / docs / code comments) is confirmed with the user in S0 — default: the user's current language. Neither Chinese nor English is hardcoded (decision point in §4; details in §12.1-8 / §12.2-9) |

## 2. When to Use

- The user wants to systematically learn a new AI project — any type: applications (text / RAG / Agent / multimodal / generative), model training, platform infrastructure, quality assurance — the mainstream-type index is in §5.3; types that do not match still apply.
- The user wants a "chapter-based learning plan document" for a project, with a uniform layout and content that fits the actual project.
- While learning, the user requires the documented state to stay consistent with the actual code artifacts.
- The skill is copied into another project / repo and generates a fresh learning plan for that project independently (no cross-pollution).

## 3. Workflow Overview (S0–S5)

| Phase | Action | Output |
|---|---|---|
| S0 Profile | Probe / ask about the project: type, size, tech stack, stage, learning goal, delivery form, environment constraints | Profile summary (written into the LEARN.md document header) |
| S1 Derive | From first principles, break down "the rings that must be walked through" → fold into a chapter map | Chapter list (count and topics open-ended, with derivation rationale) |
| S2 Render | Render the learning plan document **LEARN.md** per the §6 template spec (place it at the target project root) | LEARN.md |
| — Review gate | **The user reviews and confirms LEARN.md** (mandatory before any code is generated; see §7) | User feedback → revision → confirmed draft |
| S3 Environment | Bring the environment up per the LEARN.md environment chapter (deps / services / config); red lines in §13. **Highest hands-on chapter**: starting services and installing deps is done by the user (§16) | Runnable environment (environment-chapter artifacts marked `verified`) |
| S4 Per-chapter loop | Each chapter: align → generate / explain → hands-on points → local green-check verification → state sync → close (see §9 / §16) | Per-chapter artifacts + hands-on completion records + ledger progress + status-card updates |
| S5 Acceptance | Accept per the closing chapter of LEARN.md (tests / self-checks / doc consistency / blind rehearsal, §16.4) | Learning-complete marker (sync_event trail) |

Iron rule throughout: **no code before the review gate; each chapter's artifacts are green-checked before sync; the doc state always follows the ledger.**

## 4. S0 Project Profile (probe first, then ask — never guess)

The following dimensions must be obtained. When information is missing, **probe the project directory and existing docs first**; for what probing still cannot answer, **ask the user item by item** — never assume:

| Dimension | Question to answer | Why it shapes the design |
|---|---|---|
| Type | Which layer of §5.3 (application / model / platform / quality)? Which class? New shapes not in the table are recorded as they are. Black-box or white-box target? | Decides the kinds and order of rings |
| Scale | Number of modules, code volume; existing docs / tests / CI assets | Decides chapter count and per-chapter granularity |
| Tech stack | Language, framework, model source (local models / cloud APIs), database, containerization | Decides environment-chapter content and commands |
| Stage | Built from scratch? Extending an existing skeleton? Already live and needs evaluation / refactoring? | Decides where learning emphasis goes |
| Learning goal | Run it / test it / modify it / deliver it independently? What can the learner do alone at the end? | Decides how high the acceptance bar is |
| Delivery form | Notes only, or real code / tests / CI artifacts too? | Decides what each chapter produces |
| Environment constraints | Which services need manual startup by the user, where models and data live, which directories must never be deleted, network / proxy limits | Written into the §13 generic red lines |
| Sharing requirement | Will the artifacts / this skill be shared externally (e.g. GitHub)? Any sensitive-info boundary? | Decides whether `.engine` is committed and how secrets are handled |
| Output language | Language for the learning conversation? Language for artifacts (LEARN.md / docs / code comments)? **Default: follow the user's current language** (Chinese if the user speaks Chinese, English if English); for artifacts aimed at an international audience, English can be explicitly chosen | Decides the written language of LEARN.md and all artifacts (details in §12.1-8 / §12.2-9) |

The resulting "profile summary" goes into the LEARN.md document header (§6.1) — the factual basis for every later derivation.

## 5. S1 First-Principles Derivation → Dynamic Chapter Map (core; no template copying)

**Rule: chapter count, topics and order are decided by the profile. This skill presets no fixed chapter count and never copies another project's chapter order.**

The derivation method is "ring thinking": ask yourself — to truly understand this system and learn it from zero to the point of independently modifying it, **which closed rings must be walked through, in order**? Each ring the learner completes grants one verifiable capability.

### 5.1 Derivation Question Checklist (trim by project type)

1. What are the system's input / output boundaries? Which external dependencies (models / libraries / services) does it call?
2. Where does data come from, what does it look like, how does it enter the system (collection / ingestion / splitting / cleaning / format conversion)?
3. How many stages does the core processing split into (retrieval / generation / reasoning / planning / tool calling …)? What are the 1–2 most critical objects in each stage?
4. How do you verify "it was done right" (deterministic assertions / evaluation metrics / human criteria / gates)?
5. Does it need observability in production (traces / logs / dashboards / cost)? How do you locate problems?
6. Does it need guardrails (input / output filtering / security testing / permissions / compliance)? Do performance and cost matter?
7. How is it delivered (deployment / packaging / CI / docs wrap-up)? What is the closing acceptance criterion?

### 5.2 Rules for Folding into Chapters

| Case | Folding strategy |
|---|---|
| One ring is large (e.g. "data" covers collection + cleaning + ingestion) | Split into multiple chapters, one verifiable sub-ring each |
| Neighboring rings are all small (e.g. "prompt" + "output contract") | Merge into one chapter |
| Pure-concept ring (overview / methodology) | Stand alone as a "code-free chapter" — goals and concepts only |
| Environment / deployment-type rings | Placed at the very front (S3 environment) and the very end (delivery) respectively |

Keep each chapter within what one learning session can complete; split if a chapter is too big, merge if too small — **granularity is decided by content, not by template**.

### 5.3 Heuristic Starting Points (layered index; reference only — never copy verbatim)

All AI projects share the base skeleton "environment → main line → evaluation → deployment / closing". The table below lists only **the core rings that distinguish each mainstream type** — hints for derivation direction, **not a default template**. Real chapters must go back to the 5.1 checklist and answer for this project. **Types not listed (including new shapes) run the same 5.1 / 5.2 flow — the method's validity does not depend on matching this table.**

| Layer | Mainstream project type | Distinguishing core rings (unique beyond the base skeleton) |
|---|---|---|
| Application | LLM text apps (QA / summarization / translation / writing) | Prompt & output contract → evaluation set → regression → production monitoring |
| Application | RAG knowledge-base QA (incl. GraphRAG variants) | Document / data preparation → retrieval adaptation (chunking / embedding / recall / rerank) → retrieval quality and generation quality evaluated separately → gates |
| Application | Agents (tool calling / multi-step planning) | Tool definitions → planning loop → memory / context → guardrails → success-rate & cost evaluation |
| Application | CV apps (classification / detection / segmentation / OCR) | Data & labeling → model / API selection → vision-metric evaluation (mAP / accuracy) → inference deployment |
| Application | Speech apps (ASR / TTS / real-time voice dialogue) | Audio pipeline → service / model → speech-metric evaluation (WER / latency / MOS) → real-time verification |
| Application | Multimodal apps (image-text / video understanding) | Multimodal input pipeline → context-window & image-resolution trade-offs → cross-modal consistency evaluation |
| Application | AIGC generative tools (text-to-image / video / 3D / music) | Generation pipeline (base model + upscaling / post-processing) → subjective preference & consistency evaluation → content-safety guardrails |
| Application | Recommender systems | Features → recall → ranking → offline / online metrics & A/B testing → real-time pipeline |
| Model | Classic ML & NLP pipelines (classification / regression / NER / sentiment) | Data exploration → feature engineering → training → evaluation → serving → monitoring |
| Model | LLM fine-tuning & alignment training (LoRA / full-param / DPO / RLHF / distillation) | Training data → fine-tuning → alignment → evaluation regression (guard against catastrophic forgetting) → deployment comparison |
| Model | AI data engineering (collection / cleaning / labeling / QC) | Data sources → cleaning / dedup → labeling / QC → versioning & lineage management |
| Platform | Model inference / serving platforms (deployment / quantization / acceleration) | Model loading & batching → concurrency / latency / throughput → elasticity & monitoring |
| Platform | AI gateways & observability platforms (multi-model routing / tracing) | Routing & fallback → rate limiting / circuit breaking → call tracing & billing |
| Platform | Low-code AI application platforms (orchestration / knowledge bases / plugins) | Platform feature walk-through → orchestration chain (knowledge base / plugin) → end-to-end effect evaluation |
| Quality | AI testing & evaluation engineering (cross-cutting all layers above) | System under test → test assets (exam papers / baselines) → deterministic gates → evaluation reports → observability → security / red team → self-check closing |

### 5.4 Anti-Copy Check (mandatory after derivation)

Three self-questions; revise if any fails:
1. Were these chapters copied from some project, or derived from this project's rings? — if you cannot say "why this chapter is necessary", delete it.
2. Are there "template-filling" chapters (another project has them but this project has no corresponding ring)? — delete.
3. Are there rings "this project has, but the chapter map missed"? — add.

The derivation must be explained to the user **orally — "why these chapters, why this order"** — and may be rendered only after the review gate confirms it.

## 6. S2 Learning Plan Document Template Spec (lock the shape and writing rules, not the content)

LEARN.md is generated at the **target project root** (same level as source code; travels with the project). Layout follows this spec; if the user has an existing handbook, you may declare "layout aligned with that handbook", but **chapter content is still derived by S1**.

### 6.1 Document Header (top of LEARN.md)

| Field | Content |
|---|---|
| Document title | `# <Project Name> Learning Handbook` |
| Positioning note | ≤ 3 lines: why learn it, what you can do after, relation to the project directory |
| Profile summary | S0 profile summary (dimensions per §4: type / scale / tech stack / stage / goal / delivery form / environment constraints / sharing requirement / output language) |
| Language | Body language of this handbook (confirmed in S0; default follows the conversation language; Chinese / English, not hardcoded) |
| Progress table | Table of chapter → status (**projection**; authoritative in `.engine/state.json`) |
| Document conventions | Status-card syntax notes + pointer to this skill (optional) |
| Reading guide | How to use this document: purpose and prerequisites of each chapter, must-read / skippable suggestions, artifact and hands-on-point distribution (the entry point for humans and Agents to reuse / maintain this doc) |

### 6.2 Layout Conventions

1. Heading levels: `#` document title; `##` chapter (`Chapter X …`); `###` section (`X.Y`).
2. Key-function sections use a uniform format: `#### 📄 Source file <path>` grouped by file → functions / classes of the same file are grouped with class names; module-level functions are marked "belongs to no class". Signature tables: inputs labeled `name: type`, outputs labeled with type and structure (e.g. `tuple[float, list[str], list[str]]` = (coverage rate, hits, missing)).
3. Tables are the primary expression (file lists, comparisons, signatures, step tables); long paragraphs are compressed into tables; short paragraphs are used only when content does not fit a table.
4. Code blocks carry detailed plain-language comments (language follows the artifact language confirmed in S0: Chinese scenario = plain Chinese, English scenario = simple English; see §12.1-8); comments on external API / method calls go at the end of the calling line.
5. Every chapter closes with two fixed paragraphs: "**Chapter Completion Goal**" (acceptance-oriented, with the actual commands and green-check criteria) + "**Next-Chapter Goal**" (a one-line preview + one sentence on *why the next chapter follows this one* — the causal link that keeps chapter logic continuous). The document's last chapter is the "Closing Acceptance" chapter.
6. Doc-minimalism red line: keep only key engineering knowledge and artifact descriptions (conversational debugging and "why" back-and-forth stay out of the doc; details in §12.2-3).
7. Status-card syntax (readable by both humans and machines): `> **[st:<id>]** ✅ done (verified) · bound to: <relative path>`; enumerated values in §11.1.
8. Reference in-project files with relative paths; any referenced path that does not exist must be fixed before the review gate.
9. Zero-redundancy red line: no "XX version" labels; each fact written once; parentheses only for key notes; no filler (full details in §12.2-7; not expanded here).

### 6.3 Chapter Skeleton (default required element set; adjustable through the review gate)

| Element | Purpose |
|---|---|
| X.1 Section goal | What you can do after learning (acceptance-oriented) |
| X.2 File list → purpose | Per-item description of this chapter's **deliverable artifacts** (source / config / tests); temporary and intermediate files are not listed (see §9.1) |
| X.3 Key functions / objects | Classes and signatures grouped per source file, per §6.2 item 2 |
| X.4 Execution flow | How data flows, who calls whom, how to verify |
| X.5 Test deep-dive | What is covered, how to run, green-check criteria |
| X.6 Hands-on practice | Checklist of operations the user must perform by hand in this chapter (start services / install deps / run core commands / verify results / oral recap); the Agent only provides exact commands and judging criteria (see §16) |

> Sections inside a chapter are likewise not fixed: pure-concept / code-free chapters may declare X.2 / X.3 removed and keep only goal + concept + practice; a chapter with a special theme (e.g. "environment setup") may add its own sections — all additions / removals are declared to the user at the review gate. For chapters that drop X.2 / X.3, X.6 remains as "oral recap" (hands-on practice is part of learning; concept chapters are no exception).

## 7. Review Gate (the hard checkpoint between human and machine)

| # | Pass criteria (all must hold before entering S3) |
|---|---|
| 1 | Chapter count and topics derived from the profile; "why these chapters" already explained to the user |
| 2 | No copying trace: not a transplant of another project's chapter order |
| 3 | Document header complete (profile summary, progress table, reading guide — §6.1) |
| 4 | Table columns consistent; status-card syntax valid; all referenced paths exist |
| 5 | No "conversational debugging / why" content mixed in |
| 6 | The user explicitly replied "confirmed" or gave revision feedback (re-run the gate after revision) |
| 7 | Every chapter includes an X.6 hands-on-practice element; body text has no "XX version" labels and no filler (§6.2-9 / §12.2-7) |

If the gate is not passed, S3 environment setup and any code generation are not allowed.

## 8. S3 Environment Setup

Follow the environment chapter of LEARN.md: install deps, start services, configure secrets / middleware, import data. Read the §13 generic red lines first (especially "user-manual-start" services). **The environment chapter has the highest hands-on intensity**: hands-on points are arranged by the §16.1 levels — must-do level (daemon / GUI service startup) is never taken over; strong-practice level (dep installs, service bring-up, connectivity checks) is primarily performed by the user, with the Agent providing exact commands, parameter explanations and "ready / failed" judging criteria; the Agent falls back only after the user has been stuck three times. When everything is ready, the Agent verifies minimal connectivity once as a fallback (e.g. `--version`, health check, minimal call), registers the environment-chapter artifacts in the ledger and marks them `verified`.

## 9. S4 Per-Chapter Learning Loop (fixed rhythm per chapter; no skipping)

| Step | Action | Acceptance point |
|---|---|---|
| 1 Align | Explain this chapter's goal and engineering trade-offs; wait for user confirmation | Generation starts only after user confirmation (the user prefers discussion before coding) |
| 2 Generate / explain | Generate code or explain knowledge per the chapter; **do not dump too much at once**; **never pre-generate later chapters' code** (generate only when that chapter is reached); code minimal but sufficient, no debug residue (§12.1); also announce this chapter's X.6 hands-on checklist (§16.1) | Code follows the §12.1 minimalism and comment rules |
| 3 Verify | Dual-track verification: ① the Agent first runs local green checks (run tests / minimal calls; zero type errors is a blocking requirement); ② the most skill-building command is handed to the user as a "hands-on point" — the user executes it and the output must match the Agent's own verification | Both sets of outputs are shown to the user, and it is explained "which line counts as the green check" |
| 4 Sync | Register this chapter's artifacts in `.engine/state.json` and update the LEARN.md status card and the header progress table (§11.3) | Ledger and doc consistent |
| 5 Close | Check off the "Chapter Completion Goal" item by item; the user does the oral recap (§16.3); clean this chapter's temp files (§9.1); preview the next-chapter goal (with the causal link) | Every chapter close leaves a sync_event |

### 9.1 Artifact Cleanliness: Temp-File Identification & Cleanup (at every chapter close; re-checked at S5)

Only "deliverables the learner wants to keep / reuse / accept" are artifacts — they enter the ledger and the LEARN.md file list. Everything else is a temp file: **clean after use; never in the ledger; never in the docs**.

| Temp-file type | Examples |
|---|---|
| Intermediate conversion output | Intermediate output of extraction / conversion scripts (temp json / csv, un-ingested conversions) |
| Debug residue | Debug print output files, temp logs, commented-out code blocks, unused imports |
| Run caches | `__pycache__`, `.pytest_cache`, temp data dirs / vector stores used up by verification |
| Backups & drafts | One-off backup copies, exploration scripts, abandoned scaffolding files |

Closing flow (executed at the same point as state sync):
① Compare the directory against this chapter's X.2 file list; flag files outside the list;
② Judge each item: deliverable artifact → add to the X.2 list and the ledger; temp file → add to a cleanup list;
③ Show the cleanup list to the user in the conversation for confirmation before deleting (still respecting the "back up before changing" red line, §13-7); write a sync_event for the deletion (kind=cleanup);
④ At S5, re-check the whole project: the target project directory should contain only the LEARN.md-listed artifacts + `.engine/` + environment-required directories.

## 10. S5 Closing Acceptance

- Accept item by item against the closing chapter of LEARN.md: full test / self-check pass, doc and ledger consistent, no `verified` entry without green-check support.
- Artifact-cleanliness re-check: no temp / debug / cache residue in the directory; consistent with the LEARN.md file list (§9.1).
- **Blind-rehearsal acceptance** (§16.4): with commands and status cards hidden, the user independently runs the minimal chain end-to-end starting from environment startup; the Agent only observes and asks guiding questions — never takes over.
- Output the learning summary (in the conversation, not into the handbook): what was learned, how far the user can independently reproduce, remaining blocked items, next-step suggestions.
- If artifacts will be shared (e.g. on GitHub), run the §14 sharing check.

## 11. State Ledger & Two-Way Sync

### 11.1 Status Enumeration (the only legal values)

| code | meaning | allowed sources |
|---|---|---|
| `planned` | Planned in the doc; artifacts not yet generated | — (initial) |
| `in_progress` | Currently learning / generating | planned |
| `verified` | Artifact generated and locally green-checked | in_progress, dirty |
| `dirty` | Artifact changed but not re-verified (auto-demoted by sha256 drift) | verified |
| `blocked` | Blocked by environment / dependency; human intervention needed | any |

Migration legality: `planned → in_progress → verified`; `verified → dirty` (automatic); `dirty → verified` (requires re-running the green check); `blocked` can be entered from any state (human intervention) and returns to the actual state when resolved. **There is no shortcut between verified and dirty beyond these transitions.**

### 11.2 Ledger File `.engine/state.json` (auto-generated at runtime)

When the skill is applied to a target project, the Agent auto-creates the `.engine/` directory at the **target project root** and maintains `state.json`. **The skill file itself presets and carries no ledger example** — the ledger belongs to the concrete target project and stays separate from the skill.

Store only facts; derivable fields are not persisted; checksums use the first 12 characters of sha256:

```json
{
  "profile": { "type": "rag", "tech_stack": ["python", "vectordb"], "stage": "from-scratch" },
  "chapters": [
    { "id": "ch1", "title": "Environment & scaffolding", "kind": "code", "elements": ["files", "functions", "flow", "tests"] }
  ],
  "artifacts": [
    { "id": "art-1", "path": "src/client.py", "sha256": "a1b2c3d4e5f6", "status": "verified", "owned_by": "ch1" }
  ],
  "manual_marks": [
    { "id": "ch2", "status": "verified", "by": "user-confirm", "ts": "2026-09-02T23:40:00" }
  ],
  "sync_events": [
    { "ts": "2026-09-02T23:40:00", "kind": "push", "action": "mark art-1 verified" }
  ]
}
```

Field definitions:

| Field | Description |
|---|---|
| `profile` | S0 profile summary (type / tech_stack / stage …), archived for traceability only |
| `chapters[]` | Chapter definitions: id, title, kind (`code` = has artifacts / `concept` = code-free explainer chapter), elements |
| `artifacts[]` | Artifact registry: path (relative to the target project root), sha256, status, owned_by (owning chapter id) |
| `manual_marks[]` | Human-confirmation records (a concept chapter is done when the user confirms in the conversation; see 11.3) |
| `sync_events[]` | Audit log of sync operations: ts, kind (validate / push / pull / manual_mark / backup / conflict), action |

**Chapter status is not stored but derived** (avoids two conflicting statuses inside the ledger):

| Chapter kind | Derivation rule |
|---|---|
| code | Aggregate all its artifacts: all verified → verified; any dirty → dirty; any blocked → blocked; with planned / in_progress → the worst incomplete state |
| concept | No artifacts → the latest user-confirmation record in `manual_marks` decides (no record = planned) |

The ledger registers only deliverable artifacts (for acceptance / reuse); temp and intermediate files are not registered — their cleanup leaves only a sync_event (§9.1). The ledger only appends / updates, never silently deletes; important actions write `sync_events` for auditability. Whether `.engine/` is committed (git) is the user's call: if it holds no sensitive info, committing is recommended (learning progress travels with the repo); if it holds secrets / private data, add it to `.gitignore`.

### 11.3 Two-Way Sync Rules

**Direction A (artifact changed → doc sync)**: after each artifact / environment generation or modification, explicitly run at the action's closing point — ① recompute the artifact's sha256; ② compare with the registered value; on mismatch, demote the status to `dirty`; ③ re-run the local green check; on pass, return to `verified`; ④ update the LEARN.md status card and the progress table. **When a behavior stated in the doc (e.g. "capability X done") has no green-check-supported artifact, marking it `verified` is forbidden.**

**Direction B (doc status change → artifact actions)**: the user marks a chapter as "to learn / planned / add content" in the doc or review → the Agent parses the change into an action list: artifacts to be created → `planned`; planned chapters → scheduled for learning; concept-chapter completion confirmed → record a `manual_mark`. **When the doc declares progress ahead of the artifacts, only generate an "action list" — never mark `verified` directly.**

**Trigger timings** (no background watchers; all explicit):

| Timing | Action |
|---|---|
| Every action closing point | Right after generating code / running tests / changing the doc structure, run Direction A or B sync immediately |
| Every session start | Run `validate` (below) |
| On user request | Full validate + rebuild doc projections |

**Session-start validate flow**: ① read state.json; validate JSON legality and enum legality; ② recompute sha256 for all artifacts; demote drifters to `dirty`; ③ compare the LEARN.md status cards / progress table against the ledger; list inconsistencies; ④ summarize the dirty / blocked lists and suggested actions; ⑤ write sync_events throughout.

### 11.4 Conflict Handling (adjudication priority; never auto-overwrite)

| Conflict | Handling |
|---|---|
| C1 Doc and ledger both changed | Rebuild the doc projection from the ledger as fact; back up the two differences as evidence first, then explain the differences to the user |
| C2 Doc declares state ahead of artifacts (e.g. marked verified but the artifact is missing) | Generate an action list to complete the artifact; until completed, state follows reality (missing artifact = planned) |
| C3 Artifact modified but not verified | sha256 drift → automatic `verified → dirty`; only after a human re-confirms the green check can it return to verified |

Adjudication priority: **real green check > explicit human mark > engine inference**. The engine never auto-overwrites the first two.

### 11.5 Consistency Guarantees

① Single source of truth (the ledger; docs are projections only). ② Back up before writing; self-check after writing (table columns, status-card syntax, path existence, JSON validity). ③ Idempotent and auditable (repeated sync has no side effects; sync_events leave a trail). ④ Session-start validate as the safety net.

## 12. Code & Doc Production Rules (delivery standards from the learner's perspective)

### 12.1 Code Production Requirements (minimal + commented; execute item by item)

**Minimal code (before comments)**: write only the minimal code needed to reach this chapter's goal — prefer the standard library and the project's existing tools; no premature abstraction, no unused wrappers or "might need later" parameters; one function does one thing; no dead code, commented-out blocks or debug residue (clean debug print / log before delivery); naming is documentation — comments explain only "why", never translate syntax line by line. Comment requirements:

| # | Requirement | Example |
|---|---|---|
| 1 | **External API / method / third-party library calls: the comment must sit at the end of the calling line** — what is called, what is passed, what is returned; never pile them up at the end of the file | `resp = client.chat(messages)` `# calls the remote chat API: passes history, returns the model reply` |
| 2 | 1–3 comment lines at the head of every file: responsibility and ownership | `# Adapter layer: wraps HTTP calls to the system under test for unified use by upper layers` |
| 3 | Above every class / function definition: purpose + inputs + outputs (language follows artifacts; parameter names match the code; examples below are the Chinese scenario) | `# Computes coverage: inputs answer(str), expected_keywords(list); output (rate, hit, missing)` |
| 4 | **Plain-language comments** (language follows artifacts) per logical segment inside code blocks: "why this is done + the mental model", not line-by-line syntax restatement | `# Normalize before comparing: model output may carry punctuation/spaces; direct comparison always fails` |
| 5 | Non-obvious logic (regex, bit operations, async, state machines, algorithms, magic values) gets step comments | `# The first 12 chars uniquely identify the value; anything longer only adds noise` |
| 6 | Config / manifest files (env, yaml, toml, docker, dependency lists): every key gets an end-of-line or above-line comment | `# write_mode: dual = dual-write, compatible with older versions; new installs may drop this line` |
| 7 | No meaningless comments (`x += 1  # x plus one`); no wholesale copying of official-documentation comments | Self-evident code is not commented |
| 8 | **Comment language follows the artifact language confirmed in S0 — nothing hardcoded**: Chinese scenario → plain Chinese, no jargon piles or English abbreviations; English scenario → plain English; proper nouns (API / command / library names) stay untranslated; give analogies for hard concepts. Table examples are all Chinese-scenario; the English scenario replaces them under the same rules | `# Vector-store isolation: each test round uses an independent temp dir, like a fresh scratch sheet per exam` |

### 12.2 Doc Writing Requirements

| # | Requirement |
|---|---|
| 1 | Tables are the main expression (lists / comparisons / signatures / steps); paragraphs only for connected reasoning that tables cannot hold |
| 2 | Every chapter closes with "Chapter Completion Goal & Next-Chapter Goal"; the document's last chapter is closing acceptance |
| 3 | Keep only key engineering knowledge and artifact descriptions; **conversational debugging, "why" back-and-forth and trial-and-error never enter the doc** |
| 4 | Engineering conclusions / test summaries get one plain-language closing sentence at the original spot (the conclusion must be repeatable by a total beginner); this is "supplement in place", not a separate "plain-language version" |
| 5 | Each fact is stated once (avoids two-point drift); when doc and ledger disagree, rebuild the projection from the ledger |
| 6 | When something is hard to explain, organize it as "learner's existing experience → analogy → minimal runnable demo → real framework (marked advanced)" |
| 7 | **Zero "versions", zero filler red line**: ① no "XX version" labels in doc / file body text (e.g. "plain-language / casual / formal version") — each content is written once and is plain-language by default; splitting the same content into multiple "versions" is forbidden; ② parentheses only for key notes (why / trade-offs / analogies / how to read results); no version tags or "as stated above" filler inside parentheses; ③ delete all filler and redundancy: no transition clichés such as "let's now look at", no restating earlier text or table content, no irrelevant long quotations; merge paragraphs into tables whenever possible |
| 8 | **Highlighted, justifiable, causally continuous**: ① conclusion first, then elaboration; key information (commands / paths / acceptance criteria) bolded or on its own line, layered apart from background — readers can reuse it without reading the whole doc; ② the cut / keep test — every piece of content must support some reader action (run a command / judge / accept / maintain / debug); if you cannot answer "what does it support", delete it; never pad background for "completeness"; ③ dedupe before adding: merge into a table or delete if redundant with earlier text; skip unless necessary; ④ chapters are linked by the causal chain of "Next-Chapter Goal" (§6.2-5) — explain why this chapter follows the previous one before entering a new topic |
| 9 | **Language follows the user (confirmed in S0; see §4 "output language")**: ① LEARN.md and all docs are written in the confirmed artifact language — Chinese or English, both fine, **default follows the user's current language, nothing hardcoded**; ② the conversation (explaining / Q&A / oral recap / blind-rehearsal guidance) always uses the user's current language and switches when the user switches; ③ proper nouns, commands, error messages and API / library names stay untranslated; ④ no Chinese-English mixing within one document (sample code-block comments follow the comment rule §12.1-8) |

### 12.3 Pre-Delivery Self-Checklist (run before every artifact delivery)

- [ ] Code locally green-checked (log output pasted)? Zero type errors?
- [ ] All external API-call comments at the end of their calling lines?
- [ ] Every new file has a responsibility header; every new function has purpose / inputs / outputs?
- [ ] Table columns consistent; no conversational-debug residue; this chapter's status card synced?
- [ ] No "XX version" labels, no decorative parentheses, no filler (§12.2-7)?
- [ ] This chapter's X.6 hands-on checklist defined, and the user completed it by hand and reported the output?
- [ ] Code minimal and sufficient; no dead code or debug residue (print / log cleaned)?
- [ ] This chapter's temp files cleaned (§9.1); the LEARN.md X.2 list matches the directory?

## 13. Generic Red Lines (environment, config and change operations; extend per project profile; the following are cross-project generics)

1. Services that need user-manual startup (Docker Desktop, local model services, databases, message queues, etc.) **are always started manually by the user**; when not running, prompt the user — never auto-launch (auto-launch causes crashes).
2. Model / data directories follow what the user says; duplicate copies of the same file are not re-pulled; project data volumes / data directories are never deleted.
3. Auth and middleware configuration (e.g. write mode, secrets, proxy) follows official documentation and local measurements (change operations follow §13-7).
4. All paths are relative to the target project root; docs and ledger carry only relative paths; the skill file itself contains no absolute path.
5. Secrets / credentials go into `.env` only (never committed); `.env` is never written into docs or the ledger; run the §14 check before sharing.
6. In a learning session, skill-building operations (pulling deps / starting services / running key commands / verifying results) are performed by the user's own hand first; the Agent provides exact commands and judging criteria and acts as fallback; only purely transactional actions may be done for the user (details in §16).
7. Back up before any change; change only the specified spot; roll back on failure; list changes in a table (path + change type) for rollback checking.

## 14. Cross-Project Portability (zero-dependency guarantee & migration flow)

- **This skill has zero external dependencies**: no paths, file names, tool stacks or trademarks of any specific project are referenced; the only thing it ever creates inside a target project is the runtime-generated `.engine/` ledger.
- **Applying it to a new project**: ① make sure the skill file lives in the target repo (repo root or under `docs/`, no enforced location); ② profile that project starting from S0 (never read any old project's LEARN.md as a chapter reference); ③ generate that project's LEARN.md and `.engine/`.
- **Multi-project coexistence**: each project holds its own LEARN.md and `.engine/`, never reading or writing each other's; the skill file may sit in each repo.
- **Sharing check (e.g. on GitHub)**: before publishing, confirm the skill file contains no absolute paths, no secrets, and no private information of any project; when sharing a target project, self-check that `.env`, data volumes and secrets are not committed; carrying the `.engine/` progress is the user's call (ignore it if it holds sensitive information).

## 15. Teaching Discipline (cross-project quick view; details in §6 / §9 / §12 / §13 / §16)

> This section condenses the discipline scattered across the detail rules into a quick-view table. **It carries no new rules**; each row cites its detail source. On conflict, the detail rules win — to add or remove a rule, maintain only the cited section; this table is not expanded (prevents two-point drift).

| # | Discipline in brief | Detail source |
|---|---|---|
| 1 | Step by step: bridge concepts with the learner's existing experience → build intuition with minimal runnable demos → real frameworks marked "advanced · ideas only"; counter-intuitive points (non-determinism, why model output cannot be matched exactly) get minimal-demo intuition, not empty theory | §12.2-6 |
| 2 | Foolproof, one-step-at-a-time explanations covering the common full set; heavy use of tables and comparisons; conclusions closed in plain language a beginner can repeat | §12.2-4 |
| 3 | Align before acting: discuss the plan and engineering trade-offs (including alternatives) first; code only after confirmation; back up before changes, change only the specified spot, roll back on failure, list changes in a table | §9 step 1, §13-7 |
| 4 | Green check before delivery: local run with log proof before delivery; type errors are blocking; unverified speculation stays in the conversation | §9 step 3, §12.3 |
| 5 | Lean, clean docs: conversational debugging / "why" back-and-forth never enters the doc; every chapter closes with "Chapter Completion Goal & Next-Chapter Goal" | §6.2-5/6, §12.2-2/3 |
| 6 | No early code piling: code is generated only when that chapter is reached; never dump too much at once | §9 step 2 |
| 7 | Hands-on first: skill-building actions (start services / install deps / execute / verify / debug) are done by the user's hand; every chapter has X.6 hands-on points plus a closing blind rehearsal; never take over because automation is faster | §16 |
| 8 | Zero "versions", zero filler: no "XX version" labels; each fact written once; parentheses only for key notes | §12.2-7 |
| 9 | Artifact cleanliness: temp / intermediate / debug / cache files cleaned right after use, never in the ledger or the docs; whole-project re-check at closing | §9.1 |
| 10 | Minimal, sufficient code: only what the goal needs; no premature abstraction; no dead code or debug residue | §12.1 |
| 11 | Highlighted, reusable docs: conclusion first; content must support reader actions; cut what supports nothing; explain causal links between chapters | §6.2-5, §12.2-8 |

## 16. User Hands-On Practice (learned = can deliver independently)

In the learning pipeline the Agent handles: explaining concepts, generating code and docs, green-check self-verification, state sync and fallback debugging. **But "learned" is judged not by "the Agent ran it" but by "the user can run it themselves"** — therefore this skill embeds a "hands-on point" in every chapter (X.6 of each LEARN.md chapter): any action that builds muscle memory is handed to the user to perform first. The Agent provides exact commands, parameter explanations and output-judging criteria; the user executes by hand; the Agent falls back only when the user has been stuck three times with no resolution. Never finish the operation for the user "because automation is faster", and never skip a hands-on point because "the user is slow by hand".

### 16.1 Hands-On Levels (three tiers, arranged by skill value)

| Level | Typical actions | Who executes | Why |
|---|---|---|---|
| Must-do (daemon / GUI) — never taken over | Daemon / GUI service startup (Docker Desktop, local model services, databases, middleware consoles, etc.); admin-UI / browser operations (data import, app publishing, config toggles); actions that require an account or an interactive UI | The user's hand | Auto-launch tends to crash and teaches no troubleshooting; UI operations cannot be reliably replaced; this is daily real work |
| Strong practice — first time by hand | Pull deps / install tools (`pip install`, `npm install`, `docker pull`, `ollama pull`); run core commands (run tests, minimal calls, start scripts); read logs and results (which line is the green check, which part to read on failure) | The user executes; the Agent gives exact commands with per-parameter explanations; the user reports output; the Agent judges | Build the reflex "type command → read output → judge success / failure", not just reciting docs |
| Light practice — can automate, but must be able to explain | Repetitive verification scripts, batch regression, ledger sync, format checks | The Agent executes; the user must be able to explain "what this command / script does and why it is written this way" | Prevents "seen it, therefore know it"; the Agent may spot-check recaps anytime |

> Default: 1–3 hands-on points per chapter (mostly strong-practice level), written into that chapter's X.6 in LEARN.md; pick the most skill-building actions — do not pad with purely transactional ones. A concept chapter's hands-on point = oral recap (16.3).

### 16.2 Hands-On Execution Rhythm (embedded in the S4 loop)

1. Before entering this chapter's "verify" step, the Agent reports the X.6 checklist to the user: the action, the exact command, the expected output (what the green check looks like), and what to self-check first on failure.
2. The user executes by hand and reports the output; the Agent judges and compares it against its own green-check results; on mismatch, the user first self-checks three steps (read the error's first line → see which file / line it points at → compare against the expected output for the difference); only if still stuck does the Agent step in.
3. Only after all hands-on points are done and the outputs match can the chapter enter "sync and close" (§9 steps 4 / 5).

### 16.3 Per-Chapter Oral Recap (happens only in the conversation; never in the doc)

At each chapter close, without looking at LEARN.md commands or status cards, the user answers three questions orally; the Agent corrects and fills gaps:
1. What did this chapter get running? What was the key command, and what did the green check look like?
2. Explain this chapter's most important concept / engineering trade-off in your own words (better if you can make a layperson understand it).
3. Where did you get stuck in this chapter, and how was it resolved?

> The recap and the debugging process stay in the conversation only (consistent with the §12.2-3 doc-minimalism red line); recap notes must not be written into the doc.

### 16.4 Closing Blind Rehearsal (ultimate hands-on acceptance; a hard item in S5)

1. The user sees only LEARN.md's functional goals — all commands, code and status cards are hidden;
2. Starting from environment startup, independently run the project's minimal chain end-to-end: start services → install deps → execute → verify the green check;
3. The Agent observes throughout, asking guiding questions only ("what's next? why?"), never taking over and never handing out answers;
4. On failure, the user debugs independently via the three self-check steps; the Agent steps in only after three attempts are still stuck;
5. After success, write a sync_event (record `manual_mark`: blind rehearsal passed) into the closing acceptance.

Passing the blind rehearsal is the final evidence of "learned = can deliver independently"; if not passed, go back to the relevant chapter and add hands-on points — do not proceed to the closing summary.

## 17. Completion Criteria (when this skill has done its job)

- **New project**: a LEARN.md is delivered — chapter count and topics derived from the project's rings (able to say chapter-by-chapter "why this chapter exists"), layout and writing compliant with §6 / §12, review gate passed.
- **Per-chapter progress**: each chapter's artifacts green-check self-verified; `.engine/state.json` and LEARN.md status cards consistent; no `verified` entry without green-check support; sync_events trailed throughout.
- **Hands-on ability**: each chapter's hands-on points completed by the user's hand and oral recaps passed; closing blind rehearsal passed — the user can independently run the minimal chain from environment startup (§16.4).
- **Content quality**: LEARN.md and all artifacts carry no "XX version" labels, no decorative parentheses, no filler (§12.2-7).
- **Language consistency**: the conversation and all artifacts (docs / comments) use the language confirmed in S0; no trace of a hardcoded single language anywhere (§12.2-9).
- **Clean artifacts**: the target project directory has no temp / debug / cache residue — only the LEARN.md-listed artifacts and `.engine/`; cleanliness checks done at every chapter close and at closing (§9.1).
- **Closing**: all acceptance criteria of the closing chapter met; the session ends with "what was learned, how far the user can independently reproduce, remaining blocked items, next-step suggestions".
- **Portable**: the skill file can be copied to any new project / repo and independently generate a learning plan there, leaving no trace of the previous project.
