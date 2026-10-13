---
name: srs-ai-resolving-requirements-gaps
description: Use when material ambiguity, conflicting terminology, or unresolved decisions block a requirements artifact and need an evidence-backed interview
---

# Resolving Requirements Gaps

Use the installed `grill-with-docs` workflow to resolve gaps affecting the requested artifact. This companion supplies requirements records and handoff rules while `grill-with-docs` runs the interview. Sufficient inputs proceed directly; keep architecture exploration limited to requirements constraints.

## Load the Upstream Workflow

Invoke `grill-with-docs` as the workflow interview step: read its installed `SKILL.md` and follow it to load `grilling` and `domain-modeling`, including their relevant references. Use the runtime's skill-loading tool when available; otherwise read the installed files. Name the skills loaded so a partially loaded interview is visible.

The user has explicitly selected `grill-with-docs` for this workflow. Honor that selection at material gaps without asking again or bypassing its entrypoint. Preserve its installed invocation policy; this workflow selection does not enable unrelated automatic use.

If any dependency is unavailable, report the missing skill and installation instructions from the suite README. Keep the caller's ordinary clarification/provisional path available, but do not claim that `grill-with-docs` ran or silently substitute a local copy of its behavior.

## Requirements Context

Identify the target artifact, material gaps, existing gap IDs, and affected artifact IDs. Inspect available sources, ledger, glossary, ADRs, and relevant code before asking discoverable factual questions. Code describes current behavior, not approved intent. Reuse resolved answers from earlier sessions.

Read [Record Formats](references/record-formats.md) before recording answers. Follow `grilling` for decision prerequisites, question rounds, recommendations, and shared-understanding confirmation. Follow `domain-modeling` for terminology challenges, immediate glossary updates, and ADR eligibility and formats. Use available question tools within their limits, preserving the upstream dependency order.

## Requirements Records and Handoff

After each answered round, persist every answer and ordinary decision in the ledger, preserving exact numbers, units, exclusions, and conditions. Recommendations remain proposals until answered. Partial answers leave unaddressed questions open. Link changed decisions to affected artifacts and mark previously approved affected rows `changed`; preserve unrelated approvals.

For an unavailable stakeholder or authorized provisional draft, record explicit deferrals, impact, and the source needed for resolution. Confirm the shared understanding includes these outstanding decisions rather than treating them as resolved. Deferred blockers keep affected artifacts provisional.

For ADRs, read [ADR Traceability](references/adr-records.md) alongside the upstream format. In a read-only or chat-only environment, return equivalent records and state that they were not saved.

Hand back when every material gap is resolved or explicitly deferred and the user has confirmed the shared understanding required by `grilling`; reuse confirmation already given within that scope. This confirmation does not approve the resulting artifact. If the user pauses, return pending IDs and saved progress.

Verify that every answered question has a record and saved files contain the intended updates. Report paths (or unsaved records), resolved/deferred IDs, affected artifacts, and the calling skill to resume. Apply that skill's output format and quality gate without repeating resolved questions.
