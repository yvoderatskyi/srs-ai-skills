---
name: srs-ai-creating-ai-requirements
description: Use when running a multi-step SRS workflow, assembling traceable SRS artifacts, or coordinating requirements subskills from a vague idea
---

# Creating AI Requirements

Convert an idea or request into traceable requirements one artifact at a time, maintaining a context ledger and trace chain across human review gates. Run before architecture, planning, or code when requirements are unvalidated.

## Workflow & Routing

The orchestrator owns the context ledger and routes each step to its subskill. Build and review one artifact at a time; revise upstream artifacts when downstream work exposes contradictions. For provisional work, apply Approval and Handoff and the active subskill's provisional gate; the table's gates describe completed artifacts.

| Step | Input | Output | Subskill | Gate |
| --- | --- | --- | --- | --- |
| 1. Business task | phrase/problem | questions, Q/A/conclusion table, success criteria | `srs-ai-eliciting-business-requirements` | measurable goals; assumptions marked |
| 2. Project context | approved step 1 | actors, external systems, data flows, DOT context diagram | `srs-ai-modeling-system-context` | explicit boundary |
| 3. Functional requirements | context description | coded FR grouped by module/process/role | `srs-ai-writing-functional-requirements` | clear, testable, prioritized FRs |
| 4. Use cases | FR list | UC register, flows, PlantUML use-case diagram | `srs-ai-modeling-use-cases` | UC references FR IDs |
| 5. Data model | UC steps | glossary, data dictionary, CRUD, class/state diagrams | `srs-ai-modeling-requirements-data` | entities cover UC data |
| 6. Nonfunctional requirements | success criteria, FR, constraints | measurable NFR by category and context | `srs-ai-writing-nonfunctional-requirements` | metrics and thresholds |
| 7. SRS assembly | artifact inventory and ledger | SRS plus review report | `srs-ai-creating-ai-requirements` | Assembly and Final Review below |

**Material gaps:** When material ambiguity or conflicting terms block any step, invoke `grill-with-docs` alongside `srs-ai-resolving-requirements-gaps` (pass gap/artifact IDs and evidence; reuse resolved answers; resume the active step and gate after). Sufficient inputs proceed directly; persisted records supplement the response.

## Context Ledger

Maintain this context ledger after every step and pass relevant rows forward. During interviews, `srs-ai-resolving-requirements-gaps` updates the same ledger after each answered round (see its Record Formats reference for interview fields and storage paths):

| Field | Meaning |
| --- | --- |
| `source` | upstream source: quote, interview answer, artifact ID, or labeled assumption |
| `decision` | requirement, term, actor, entity, constraint, or question |
| `ids` | linked goal/FR/UC/entity/NFR identifiers |
| `status` | `proposed`, `approved`, `rejected`, `changed` |
| `risk` | ambiguity, contradiction, uncertainty, or missing stakeholder confirmation |
| `artifact/version` | artifact location and reviewed revision |
| `approval evidence` | reviewer and acceptance message/source, or `pending` |

The **trace chain** links `source -> goal -> FR -> UC -> entity -> NFR -> SRS section`. Keep it intact across every artifact.

## Approval and Handoff

- Record `approved` only when the user or an identified authorized reviewer explicitly accepts an artifact or decision. Store reviewer, message/source, and version in `approval evidence`. Existing approval applies within its stated scope; drafting authorization, cognitive simulation, and silence leave items `proposed`.
- Start at the requested step using available artifacts. Pass approved rows with their IDs and evidence. For an authorized provisional draft, also pass `proposed` rows and unresolved questions with their status intact; dependent conclusions remain `proposed`. Follow the active subskill's clarification branch when inputs are insufficient.
- When an upstream artifact changes, mark affected approved rows `changed`, identify downstream references by ID, and revise them before seeking renewed approval for the changed scope. Preserve unaffected approvals and stable IDs.
- Finish each step by recording its artifact version, gate result, unresolved decisions, and ledger changes. A completed draft may be handed forward as provisional; approval is a separate recorded decision.

## Assembly and Final Review

1. **Inventory**: List business context, system context, FRs, UCs, data artifacts, NFRs, constraints, and glossary with location/version and disposition (`approved`, `provisional`, `changed`, `rejected`, `missing`, or `not applicable` with reason). Request only missing decisions that block the deliverable.
2. **Assemble**: Build sections for purpose and goals, scope and context, functional requirements, use cases, data, nonfunctional requirements, constraints, glossary, traceability, and unresolved decisions. Preserve source IDs and approval status. Mark missing sections explicitly and justified exclusions as `not applicable`.
3. **Traceability table**: Link each included goal, FR, UC, entity, and NFR to its upstream source and applicable downstream artifacts/SRS sections. Give every missing or inapplicable link a reason or issue ID.
4. **Quality checks**: Verify every applicable section and link against the table below. Record each failure in a review report with issue ID, affected IDs/sections, impact, and required resolution. Reconcile contradictions before declaring affected artifacts approved.

| Check | Pass condition |
| --- | --- |
| Completeness | goals, actors, FR, UC, data, NFR, constraints, glossary accounted for |
| Trace chain | FR -> source; UC -> FR; entity -> UC; NFR -> goal, success criterion, constraint, risk, UC context, stakeholder statement, or approved assumption |
| Testability | vague terms replaced with measurable thresholds or testable behaviors |
| Consistency | names, IDs, actors, modules, and entities match across artifacts |
| Feasibility | risks, dependencies, boundaries, and open questions recorded |

5. **Release gate**: Return a **draft SRS** when any required artifact is missing/provisional/changed/rejected, a blocking review issue remains, or assembly approval is absent. Label an SRS **final** only when all required artifacts are approved (or explicitly accepted as not applicable), blocking issues are resolved, and an authorized reviewer has accepted the assembled version. List any explicitly accepted nonblocking open issues.
