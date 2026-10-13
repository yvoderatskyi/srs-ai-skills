# SRS Skills

Codex skill suite for AI-assisted software requirements work, based on the workflow from "How to write an AI technical specification from one customer phrase": https://systems.education/ai-ts

The suite treats AI as a systems-analysis partner, not an autonomous SRS writer. It builds chained artifacts with explicit context, traceability, uncertainty handling, and human review.

## Workflow

Start with `srs-ai-creating-ai-requirements`. It owns the context ledger and routes detailed artifact work to focused subskills.

| Step | Artifact | Skill |
| --- | --- | --- |
| 1 | Business task, questions, success criteria | `srs-ai-eliciting-business-requirements` |
| 2 | System boundary, actors, external systems, context flows | `srs-ai-modeling-system-context` |
| 3 | Functional requirements | `srs-ai-writing-functional-requirements` |
| 4 | Use cases and use-case diagram | `srs-ai-modeling-use-cases` |
| 5 | Glossary, data dictionary, CRUD, class/state diagrams | `srs-ai-modeling-requirements-data` |
| 6 | Measurable nonfunctional requirements | `srs-ai-writing-nonfunctional-requirements` |
| 7 | SRS assembly and review | `srs-ai-creating-ai-requirements` |

## Installation

Install all eight `srs-ai-*` skill directories together into your agent's skill directory, preserving each directory's contents, including `references/`. The seven artifact skills use `grill-with-docs` for interviews and `srs-ai-resolving-requirements-gaps` for requirements records and handoffs. This workflow requires the upstream `grill-with-docs`, `grilling`, and `domain-modeling` skills from `mattpocock/skills`.

Requested upstream installation command:

```bash
npx skills@latest add mattpocock/skills --skill=grill-with-docs
```

Verify all three skills are installed. The `grill-with-docs` entrypoint only loads its two dependencies; installing the wrapper alone is insufficient. The installer used in this session installed all 38 repository skills despite the selection flag and reported overwrites, so inspect its installation summary rather than assuming a selective install.

This workflow explicitly selects `grill-with-docs` as its interview step. At material gaps, load its entrypoint and follow it to load `grilling` and `domain-modeling`. Keep the upstream invocation policy unchanged; no repeated selection is needed during the authorized workflow.

## Persistent Interviews

The seven-stage workflow is unchanged. At any stage, a material gap activates `grill-with-docs`, with `srs-ai-resolving-requirements-gaps` providing ledger and handoff guidance; sufficient source material proceeds directly. It inspects available evidence, uses upstream question rounds and recommendations, saves answers, and returns to the calling skill. Questions dependent on unanswered decisions wait for a later round.

The interview step uses [AI Hero's grill-with-docs workflow](https://www.aihero.dev/skills-grill-with-docs). Upstream owns interview behavior, glossary formatting, and ADR discipline; the suite adds durable ordinary answers, requirements traceability, and artifact handoffs. Shared-understanding confirmation follows upstream grilling and remains separate from artifact approval.

The skill reuses established project paths. Defaults are:

- `docs/requirements/context-ledger.md`: every interview answer, pending decision, evidence, and affected artifact link; updated after each answered round.
- `GLOSSARY.md`: settled domain vocabulary; an existing `GLOSSARY-MAP.md` determines context-specific locations.
- `docs/adr/`: only settled decisions that are costly to reverse, require historical explanation, and involve a real trade-off.

Files are created only when there is content, in the user's project rather than the installed skills. Read-only and chat-only sessions return explicitly unsaved records. Resolving an answer does not approve an artifact; deferred blockers preserve provisional status.

## Core Rules

- Do not generate a final SRS from one vague phrase.
- Build one artifact at a time and pass approved context forward.
- Keep a context ledger with source, decision, IDs, status, and risk.
- Mark assumptions, uncertainty, and missing sources instead of smoothing them into confident requirements.
- Preserve traceability across business goals, FRs, UCs, data entities, and NFRs.

## Skill Layout

Each skill directory contains:

- `SKILL.md`: the reusable skill instructions.
- `pressure-scenarios.md`: failure scenarios and verification targets used to evaluate the skill.
- `references/`, where present: packaged guidance loaded through conditional pointers in `SKILL.md`.

`pressure-scenarios.md` files are maintenance tests, not runtime references. They document failure modes for editing and reviewing skills; normal skill execution uses `SKILL.md` and its linked runtime references.

Planning docs are in `docs/plans/`.

## Example Usage

Full walk-through: [docs/examples/article-workflow.md](docs/examples/article-workflow.md)

## Validation

Run these checks after editing skills:

```bash
for f in */SKILL.md; do
  awk 'NR==1&&$0!="---"{bad=1} NR==2&&$0!~/^name: [A-Za-z0-9-]+$/{bad=1} NR==3&&$0!~/^description: Use when /{bad=1} NR==4&&$0!="---"{bad=1} END{exit bad}' "$f" || exit 1
done
```

Check orchestrator routing:

```bash
rg -n "srs-ai-eliciting-business-requirements|srs-ai-modeling-system-context|srs-ai-writing-functional-requirements|srs-ai-modeling-use-cases|srs-ai-modeling-requirements-data|srs-ai-writing-nonfunctional-requirements|srs-ai-resolving-requirements-gaps" srs-ai-creating-ai-requirements/SKILL.md
```

Check traceability language:

```bash
rg -n "source|trace|ID|context ledger|assumption|uncertainty" */SKILL.md
```

The checks above are static packaging checks, not behavioral validation. The gap-resolution skill's pressure scenarios cover interview rounds, persistence, terminology, revisions, and handoff fidelity. Record which scenarios were actually executed and their outcomes separately from these checks.
