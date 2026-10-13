---
name: srs-ai-resolving-requirements-gaps
description: Use when material ambiguity, conflicting terminology, or unresolved decisions block a requirements artifact and require a persistent interview
---

# Resolving Requirements Gaps

Run `grill-with-docs` to resolve material gaps blocking the target requirements artifact while persisting context ledger, glossary, and ADR trace records. Sufficient inputs proceed directly; scope codebase exploration to requirements constraints.

## 1. Load the Upstream Workflow

Invoke `grill-with-docs` as the workflow interview entrypoint: load its `SKILL.md` and follow it to load `grilling` and `domain-modeling` (with their relevant references) via the runtime skill tool or file read. Name the loaded skills so any missing dependency is visible.

Honor the workflow's selection of `grill-with-docs` at material gaps immediately while preserving its installed invocation policy outside this workflow. If any upstream skill is missing, report the missing dependency and installation command from `README.md`, and fall back to the calling skill's ordinary clarification/provisional path without claiming `grill-with-docs` ran.

## 2. Prepare Requirements Context

Identify the target artifact, material gaps, existing gap IDs, and affected artifact IDs. Inspect available sources, context ledger, glossary, ADRs, and relevant code before asking discoverable factual questions (treat code as current behavior, not approved intent; surface any mismatch with stated requirements). Reuse resolved answers from earlier rounds.

Read [Record Formats](references/record-formats.md) before recording answers, and [ADR Traceability](references/adr-records.md) when a decision qualifies for an ADR under `domain-modeling`. Follow `grilling` for prerequisite ordering, question rounds, recommendations, and shared-understanding confirmation; follow `domain-modeling` for terminology challenges and immediate glossary updates.

## 3. Persist Records & Hand Off

After each answered round, update the context ledger per [Record Formats](references/record-formats.md), preserving exact numbers, units, endpoints, exclusions, conditions, and assumption/uncertainty labels. For unavailable stakeholders or authorized provisional drafts, record explicit deferrals with blocking impact and required source, and include them in the shared-understanding confirmation. In read-only or chat-only sessions, return the formatted records inline and state that they were not saved.

Hand back when every material gap is resolved or explicitly deferred and the user has confirmed the shared understanding required by `grilling` (reusing in-scope confirmation if already given; if the user pauses, return pending IDs and saved progress). Verify saved files match the intended updates, report paths (or unsaved records), resolved/deferred IDs, and affected artifacts, and resume the calling skill's output format and quality gate.
