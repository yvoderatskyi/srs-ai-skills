# Article Workflow Example

This example follows the article's demonstration phrase:

```text
Help me make GPT so invisible that people stop fearing the singularity.
```

Use the skills as an artifact chain, not as one large SRS prompt.

## 1. Start the Workflow

```text
Use srs-ai-creating-ai-requirements.

Initial customer phrase:
"Help me make GPT so invisible that people stop fearing the singularity."

Do not generate an SRS yet. Create the context ledger and route me to the first artifact step.
```

## 2. Elicit Business Requirements

```text
Use srs-ai-eliciting-business-requirements.

Business idea:
"Help me make GPT so invisible that people stop fearing the singularity."

Create interview questions, a Q/A/conclusion table template, measurable success criteria, assumptions, and risks.
If information is missing, stop before drafting requirements.
```

Expected focus: goals, fear drivers, target users, acceptable autonomy, transparency, safety, escalation rules, and success metrics.

## 3. Model System Context

```text
Use srs-ai-modeling-system-context.

Approved context:
- Goal: AI assistance should feel predictable and non-intrusive.
- Users: everyday users, professional users, administrators.
- External systems: smart home, calendar, communication tools, professional AI agents.
- Open issue: exact autonomy boundaries are not confirmed.

Produce actors, external systems, data flows, unresolved boundary questions, and a DOT context diagram.
```

## 4. Write Functional Requirements

```text
Use srs-ai-writing-functional-requirements.

Input:
- Context model for Invisible AI
- Actor: everyday user
- Module: ambient assistance

Write MVP functional requirements only for this actor/module.
Use stable FR IDs, source links, priority, and testable wording.
Preserve NFR-like material in NFR Candidates.
```

Example requirement shape:

```text
FR-001 | The system shall detect when the user is asking for background assistance and respond without opening a full chat interface. | Source: BR-002, CTX-FLOW-01 | High
```

## 5. Model Use Cases

```text
Use srs-ai-modeling-use-cases.

Input FRs:
FR-001 ambient assistance
FR-002 explain autonomous action
FR-003 escalate uncertainty to the user

Create a UC register, FR coverage table, main/alternate/error flows, and PlantUML use-case diagram.
```

Example use-case candidates from the article's scenario include naming the AI for friendly communication, activating an autonomous alarm clock, teaching the AI a new function, generating a report by voice request, and ordering flowers for a birthday.

## 6. Model Requirements Data

```text
Use srs-ai-modeling-requirements-data.

Input:
- UC register and UC flows for Invisible AI
- FR IDs and context model

Create glossary, data dictionary, entity source links to UC steps, CRUD matrix, and only justified class/state diagrams.
Do not invent unsupported entities or states.
```

Possible entities might include `UserPreference`, `AutonomousAction`, `ExplanationRequest`, and `TrustSignal`, but each must trace to a UC step or requirement.

## 7. Write Nonfunctional Requirements

```text
Use srs-ai-writing-nonfunctional-requirements.

Input:
- Success criteria
- FRs
- Risks: user fear, over-automation, lack of transparency
- Operating context: ambient AI interactions across user devices

Create measurable NFRs with NFR IDs, category, threshold, environment, source link, and verification method.
```

Example NFR shape:

```text
NFR-001 | Usability | 90% of first-time users shall understand why an autonomous action occurred within 10 seconds of viewing its explanation. | Environment: mobile and desktop | Source: SC-003, RISK-002 | Verify by moderated usability test
```

## 8. Assemble and Review

```text
Use srs-ai-creating-ai-requirements.

Assemble the approved artifacts into an SRS outline.
Then review for completeness, consistency, testability, traceability, and feasibility.
Report missing sections, contradictions, unclear requirements, and open questions.
```

## Worked Gap-Resolution Handoff

During step 7, suppose the stakeholder says: "Reminder dispatch needs to be fast." The NFR skill finds that the target and load are missing and uses `grill-with-docs` as the interview step, loading its entrypoint and dependencies. Alongside it, `srs-ai-resolving-requirements-gaps` supplies the requirements ledger and handoff rules.

First inspect the glossary and source material. If "dispatch" is undefined, ask what event completes dispatch before asking about its latency. Recommend provider acceptance as a measurable endpoint, explaining that patient delivery would need different evidence. The user settles the term as provider acceptance. Save that definition with its source in the canonical glossary immediately.

Next ask for the target and load with a clearly provisional recommendation. The user answers:

> p95 <= 60 seconds from scheduled send time to provider acceptance at 10,000 appointments/hour; exclude patient delivery latency. Verify with a load test.

Save the answer in `docs/requirements/context-ledger.md` under a stable ID such as `Q-002`, with `resolution: resolved`, affected artifact `NFR-001`, and source pointing to the user's answer. The resulting artifact remains proposed until explicitly accepted. This ordinary decision needs no ADR unless all three ADR conditions hold.

After the user confirms the shared understanding under the upstream interview rules, resume the NFR skill. This confirmation is separate from artifact approval. Its output preserves the answer:

| NFR ID | Status | Quality category | Requirement | Threshold/metric | Operating context/environment | Source link | Verification method | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| NFR-001 | confirmed | Performance | Dispatch reminders from scheduled send time to provider acceptance within the stated threshold. | p95 <= 60 seconds | 10,000 appointments/hour | Q-002; dispatch definition from Q-001 | Load test | Excludes patient delivery latency; artifact approval pending |

Here `confirmed` describes evidence for the NFR fields, not approval of the assembled artifact. Later SRS assembly carries the same percentile, bound, endpoints, load, exclusion, and source IDs forward. A resumed session reads these records rather than asking the same questions again. In a read-only session, return the equivalent records and say they have not been saved.
