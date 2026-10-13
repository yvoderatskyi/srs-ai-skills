---
name: srs-ai-creating-ai-requirements
description: Use when turning vague product ideas or stakeholder requests into traceable requirements, SRS artifacts, or requirements-analysis workflows
---

# Creating AI Requirements

## Material Gaps

When material ambiguity or conflicting terminology blocks this artifact, use `grill-with-docs` for the interview. Read `srs-ai-resolving-requirements-gaps` for the requirements ledger and handoff rules alongside it. Pass existing gap IDs, evidence, and affected artifact IDs; reuse resolved answers. After the interview, resume this skill's output and quality gate. Sufficient inputs proceed directly; persisted records supplement the response format below.

## Overview

Use AI as a systems-analysis partner, not an autonomous SRS writer. Convert a vague idea into requirements through chained artifacts, a trace chain, and human review.

Based on the SRS-style article "How to write an AI technical specification from one customer phrase" at https://systems.education/ai-ts.

## When to Use

- Stakeholder gives a vague product idea or problem, not requirements.
- Need AI-assisted SRS, FR/NFR, use cases, context diagrams, UML, data model, CRUD matrix, or RTM.
- Need requirements under high uncertainty, limited stakeholder access, or presales speed.
- Do not use for coding tasks, implementation plans, or architecture decisions without first producing and validating requirements.

## Core Rule

Build and review one artifact at a time. Use the approval and handoff rules below to advance; revise earlier artifacts when later work reveals contradictions.

## Workflow

| Step | Input | Output | Gate |
| --- | --- | --- | --- |
| 1. Business task | phrase/problem | questions, Q/A/conclusion table, success criteria | measurable goals; assumptions marked |
| 2. Project context | approved step 1 | actors, external systems, data flows, DOT context diagram | explicit boundary |
| 3. Functional requirements | Context description | coded FR grouped by module/process/role | Each FR is clear, testable, prioritized |
| 4. Use cases | FR list | UC register, flows, PlantUML use-case diagram | UC references FR IDs |
| 5. Data model | UC steps | glossary, data dictionary, CRUD, class/state diagrams | entities cover UC data |
| 6. Nonfunctional requirements | success criteria, FR, constraints | measurable NFR by environment, external quality, usage quality | metrics and thresholds |
| 7. SRS assembly | artifact inventory and ledger | SRS plus review report | Assembly and Final Review criteria below |

For provisional work, apply Approval and Handoff and the active skill’s provisional gate; the table’s gates describe completed artifacts.

## Step Skill Routing

The orchestrator keeps ownership of the context ledger and routes detailed artifact work to subskills.

| Need | Use |
| --- | --- |
| material gaps requiring an interview and documented decisions | `grill-with-docs` with `srs-ai-resolving-requirements-gaps` for records/handoff |
| clarify business task, interview questions, goals | `srs-ai-eliciting-business-requirements` |
| system boundary, actors, external systems, context diagram | `srs-ai-modeling-system-context` |
| FR list, modules, priorities, acceptance-ready requirements | `srs-ai-writing-functional-requirements` |
| UC register, main/alternate/error flows, use-case diagram | `srs-ai-modeling-use-cases` |
| glossary, data dictionary, CRUD matrix, class/state diagrams | `srs-ai-modeling-requirements-data` |
| measurable quality attributes, constraints, NFR thresholds | `srs-ai-writing-nonfunctional-requirements` |

## Required Context Ledger

Maintain this ledger after every step and pass relevant rows forward. During interviews, the gap-resolution skill updates the same ledger after each answered round; its Record Formats reference defines the additional interview fields and default storage location:

| Field | Meaning |
| --- | --- |
| `source` | quote, interview answer, artifact ID, or assumption |
| `decision` | requirement, term, actor, entity, constraint, or question |
| `ids` | linked goal/FR/UC/entity/NFR identifiers |
| `status` | proposed, approved, rejected, changed |
| `risk` | ambiguity, contradiction, missing stakeholder confirmation |
| `artifact/version` | artifact location and reviewed revision |
| `approval evidence` | reviewer and acceptance message/source, or pending |

The trace chain is the linked path from source material to goal, FR, UC, entity, NFR, and SRS section. Keep it intact across every artifact.

## Approval and Handoff

- Record approval only when the user or an identified authorized reviewer explicitly accepts an artifact or decision. Store the reviewer, approval message/source, and artifact version in the ledger. Existing approval applies within its stated scope; drafting authorization and silence leave items `proposed`.
- Start at the requested step using available artifacts. Pass approved rows with their IDs and evidence. For an authorized provisional draft, also pass proposed rows and unresolved questions with their status intact; dependent conclusions remain proposed. Follow the active subskill’s clarification branch when inputs are insufficient.
- When an upstream artifact changes, mark the affected approved rows `changed`, identify downstream references by ID, and revise them before seeking renewed approval for the changed scope. Preserve unaffected approvals and stable IDs.
- Finish each step by recording its artifact version, gate result, unresolved decisions, and ledger changes. A completed draft may be handed forward as provisional; approval is a separate recorded decision.

## Assembly and Final Review

1. Inventory business context, system context, FRs, UCs, data artifacts, NFRs, constraints, and glossary. For each, record its location/version and disposition: approved, provisional, changed, rejected, missing, or not applicable with a reason. Include existing artifacts; request only missing decisions that block the requested deliverable.
2. Assemble sections for purpose and goals, scope and context, functional requirements, use cases, data, nonfunctional requirements, constraints, glossary, traceability, and unresolved decisions. Preserve source IDs and approval status. Mark missing sections explicitly and justified exclusions as not applicable.
3. Build a traceability table linking each included goal, FR, UC, entity, and NFR to its source and applicable downstream artifacts/SRS sections. Give every missing or inapplicable link a reason or issue ID.
4. Apply Quality Checks to every applicable section and link. Record each failure in a review report with issue ID, affected IDs/sections, impact, and required resolution. Reconcile contradictions before declaring their affected artifacts approved.
5. Return a **draft SRS** when any required artifact is missing/provisional/changed/rejected, a blocking review issue remains, or assembly approval is absent. Label an SRS **final** only when all required artifacts are approved (or explicitly accepted as not applicable), blocking issues are resolved, and an authorized reviewer has accepted the assembled version. List any explicitly accepted nonblocking open issues.

## Prompt Pattern

Use this structure for every artifact prompt:

```text
Role: Act as an experienced systems analyst.
Task: Produce only [artifact] for [system/module/role].
Context: [ledger rows + previous artifact, preserving approval/provisional status]
Rules: use these IDs, output format, naming rules, priority scheme, and trace links.
Uncertainty check: if required information is missing, either ask focused clarification questions or generate a clearly provisional artifact with unresolved questions when the active step allows that.
Quality gate: verify completeness, consistency, testability, and trace chain.
Output: [exact table, Markdown, DOT, PlantUML, or SRS section only].
```

## Example

Input idea: "Help clinics reduce missed appointments."

Step 1 output is not FRs. First produce interview questions and measurable success criteria: reduction target, appointment types, channels, cancellation policy, user groups, legal constraints, integrations. Mark invented detail as an assumption.

## Quality Checks

| Check | Pass condition |
| --- | --- |
| Completeness | goals, actors, FR, UC, data, NFR, constraints, glossary |
| Trace chain | FR -> source; UC -> FR; entity -> UC; NFR -> success criterion, constraint, risk, goal, use-case context, stakeholder statement, or approved assumption |
| Testability | vague terms have measurable thresholds |
| Consistency | names, IDs, actors, modules, entities match |
| Feasibility | risks, dependencies, boundaries, open questions included |
