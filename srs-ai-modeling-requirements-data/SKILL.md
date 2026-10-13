---
name: srs-ai-modeling-requirements-data
description: Use when deriving a requirements glossary, data dictionary, entity source links, CRUD matrix, or class/state diagrams from use cases
---

# Modeling Requirements Data

Turn approved use cases, FRs, actor models, business rules, and approved assumptions into traceable requirements data artifacts. Keep the trace chain visible from UC step to entity, attribute, CRUD rule, and diagram, routing any unsupported candidate to Unresolved Data Questions.

**Material gaps:** When material ambiguity or conflicting terms block this artifact, invoke `grill-with-docs` alongside `srs-ai-resolving-requirements-gaps` to update the context ledger and glossary (pass gap/artifact IDs and evidence; reuse resolved answers; resume here after). Sufficient inputs proceed directly; persisted records supplement the response format below.

## Required Output

Produce these six sections in order:

### 1. Glossary

Define every domain term used in entities, attributes, statuses, identifiers, business rules, and diagrams. Reuse and link the canonical project glossary (following `GLOSSARY-MAP.md` when present); follow `srs-ai-resolving-requirements-gaps` Record Formats for newly settled terms, or use the inline table below when file persistence is unavailable. Keep uncertain definitions in the context ledger and Unresolved Data Questions and link those question IDs here rather than presenting proposed terms as canonical:

| Term | Definition | Source |
| --- | --- | --- |

### 2. Data Dictionary

Document every supported entity and attribute using requirement-level types and rules (include implementation fields only when required by a UC, audit rule, integration, or business constraint):

| Entity | Attribute | Type/format | Required? | Allowed values/rules | Source |
| --- | --- | --- | --- | --- | --- |

Every entity and attribute must cite a UC step, FR, business rule, stakeholder statement, or approved assumption ID.

### 3. Entity Source Links

Justify why each entity exists:

| Entity | Supporting UC step(s) | Supporting FR/rule/source | Notes |
| --- | --- | --- | --- |

- Link each entity to one or more UC steps with stable IDs (`UC-001 step 3`), or an explicit approved requirement source.
- Move any entity, attribute, relationship, state, transition, or implementation-convenience candidate lacking a requirement source to Unresolved Data Questions.

### 4. CRUD Matrix by Actor/Use Case

Account for create, read, update, and delete/archive behavior across every dictionary entity, actor, and use case:

| Actor | Use case | Entity | Create | Read | Update | Delete/archive | Source |
| --- | --- | --- | --- | --- | --- | --- | --- |

- Populate cells with `yes`, `no`, or `unclear`.
- Route entities with zero CRUD coverage and any missing create, read, update, delete/archive, retention, correction, or ownership rules to Unresolved Data Questions.

### 5. Diagrams, If Justified

Include a **class diagram** (when relationships, multiplicity, ownership, or composition require validation) or a **state diagram** (when lifecycle states, transitions, guards, or terminal outcomes require validation) only when it clarifies reviewed requirements; otherwise state why diagrams are omitted. Every diagram entity, relationship, state, guard, and transition must trace to a supported UC step, FR, or rule; route unsupported candidates to Unresolved Data Questions.

### 6. Unresolved Data Questions

Record every missing, unsupported, or conflicting data decision:

| Question ID | Location | Question | Blocks | Send back to |
| --- | --- | --- | --- | --- |

Name the clarification source in `Send back to` (`use case`, `FR`, `business rule`, `stakeholder`, `integration contract`, or `retention policy`).

## Quality Gate

Before returning, reconcile all Data Dictionary entities with Entity Source Links and CRUD Matrix coverage, verify every term and diagram element against the Glossary and supported UC/FR sources, and confirm every missing or unsupported decision has a row in Unresolved Data Questions.
