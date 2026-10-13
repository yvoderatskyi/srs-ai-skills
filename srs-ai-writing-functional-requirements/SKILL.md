---
name: srs-ai-writing-functional-requirements
description: Use when writing or auditing traceable functional requirements (FRs) and routing NFR candidates from business or system context
---

# Writing Functional Requirements

Turn approved business context, system context, use-case notes, or stakeholder statements into testable functional requirements. Keep the trace chain visible from upstream source to each FR and downstream to use cases and data.

**Material gaps:** When material ambiguity or conflicting terms block this artifact, invoke `grill-with-docs` alongside `srs-ai-resolving-requirements-gaps` to update the context ledger (pass gap/artifact IDs and evidence; reuse resolved answers; resume here after). Sufficient inputs proceed directly; persisted records supplement the response format below.

## Output Format

Group FRs by the clearest lens for the system: **Module** (product/boundary areas), **Process** (workflow stages), or **Role** (distinct actor responsibilities).

Within each group, produce the FR table:

| FR ID | Requirement | Source/context link | Priority | Notes |
| --- | --- | --- | --- | --- |

Route any nonfunctional or quality-attribute source statements into a separate **NFR Candidates** table:

| NFR Candidate ID | Statement | Source/context link | Suggested route | Notes |
| --- | --- | --- | --- | --- |

## FR & Testability Rules

- **Stable IDs**: Assign persistent IDs (`FR-001`, `FR-002`, or established module prefixes) that survive revisions.
- **Source links**: Give every FR one primary upstream source/context link (quote, interview answer, `BR-###`, `CTX-###`, `UC-###`, or labeled assumption `ASM-###`), with secondary links in `Notes`. For provisional FRs lacking a source, write `Missing - open issue OI-###`.
- **Priority**: Assign `Must`, `Should`, `Could` (or the project's established scheme) to every FR.
- **Single observable behavior**: State what the system validates, calculates, displays, stores, sends, receives, restricts, or logs—one behavior per FR, with trigger/condition, actor/system action, and expected result.
- **Acceptance-testable**: Replace vague terms (`easy`, `fast`, `secure`, `robust`, `intuitive`, `support`, `manage`, `appropriate`, `as needed`) with concrete conditions. Any phrasing is valid if it maps without new facts to:
  ```text
  Given <condition/source context>, when <actor or event> occurs, the system shall <observable behavior/result>.
  ```
- **Uncertainty & open issues**: Record assumptions, uncertainty, and open issues (`OI-###` with the missing source or decision) in `Notes`.

## Quality Gate

Before returning, verify every row against the FR & Testability Rules: each FR states one testable behavior with a stable ID, priority, and concrete source link (or `Missing - open issue OI-###`); every supplied behavior is accounted for as an FR or reasoned open issue; and all quality-attribute statements live in `NFR Candidates` with their source links and suggested routes.
