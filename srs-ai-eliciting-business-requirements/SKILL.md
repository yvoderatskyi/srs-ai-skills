---
name: srs-ai-eliciting-business-requirements
description: Use when clarifying vague business ideas, stakeholder requests, goals, risks, assumptions, or success criteria before requirements
---

# Eliciting Business Requirements

Use this skill to turn uncertain business input into validated business requirements. Use the branch selection below to determine the deliverable.

## Material Gaps

When material ambiguity or conflicting terminology blocks this artifact, use `grill-with-docs` for the interview. Read `srs-ai-resolving-requirements-gaps` for the requirements ledger and handoff rules alongside it. Pass existing gap IDs, evidence, and affected artifact IDs; reuse resolved answers. After the interview, resume this skill's output and quality gate. Sufficient inputs proceed directly; persisted records supplement the response format below.

## Required Extraction

Extract and maintain these fields:

| Field | What to capture |
| --- | --- |
| Business problem | The pain, opportunity, or decision the work addresses |
| Stakeholders | Decision makers, users, operators, affected teams, and unavailable stakeholder groups |
| Goals | Desired business outcomes, not solution features |
| Constraints | Fixed deadlines, systems, policies, budgets, legal limits, and operating boundaries |
| Success criteria | Measurable outcomes that define whether the business goal was achieved |
| Assumptions | Any invented, inferred, simulated, or unconfirmed detail |
| Risks | Ambiguity, missing stakeholder access, contradictory evidence, feasibility concerns, and validation gaps |

## Clarification First

Extract available evidence first, then use small question sets to resolve material gaps:

| Topic | Example questions |
| --- | --- |
| Problem | What business pain should this solve, and who feels it today? |
| Stakeholder | Who approves success, who uses the result, and who may object? |
| Goal | Which measurable outcome matters most: cost, revenue, risk, speed, quality, satisfaction, or compliance? |
| Constraint | What deadlines, systems, policies, budgets, or legal limits are already fixed? |
| Risk | What could make these requirements wrong or unusable? |

Select one branch after extraction:

- **Clarification:** material inputs remain missing or uncertain and provisional drafting is not authorized. Return only Known Context, Focused Questions, and Assumptions and Risks. Account for every extraction field as known, unknown, or not applicable with a reason; ask about material unknowns. This branch completes when the gaps and confirmation needs are explicit.
- **Drafting:** available evidence resolves material gaps, or the user has explicitly authorized provisional requirements. Use the full output below. Mark inferred answers and unresolved decisions as assumptions; identify unavailable stakeholders and the confirmation needed. Authorization to draft does not confirm assumptions.

## Output Format

For the drafting branch, produce these sections in order. Use `None` for Focused Questions when the supplied evidence is sufficient:

1. Known Context
2. Focused Questions
3. Q/A/Conclusion Table
4. Draft Business Requirements
5. Measurable Success Criteria
6. Assumptions and Risks

Use this table for answers and conclusions:

| ID | Question | Answer or assumption | Conclusion | Confidence | Follow-up |
| --- | --- | --- | --- | --- | --- |

Use `Answer or assumption` to distinguish confirmed stakeholder input from invented details. Conclusions must trace to an answer, source note, or labeled assumption.
Keep the trace chain visible from question to conclusion to requirement.

## Business Requirements Rules

- Keep requirements at the business level: outcomes, policies, decisions, constraints, and user/business capabilities.
- Label likely goals as assumptions until confirmed.
- Each requirement must link to a conclusion ID.
- Each success criterion must have a metric, target, timeframe, and source or assumption. For an unresolved field, record a linked question and mark the criterion provisional rather than inventing a value.
- Preserve uncertainty rather than smoothing it into confident language.

## Minimal Requirement Template

| ID | Requirement | Source conclusion | Priority | Uncertainty |
| --- | --- | --- | --- | --- |

## Success Criteria Template

| ID | Metric | Target | Timeframe | Source or assumption |
| --- | --- | --- | --- | --- |

## Quality Check

Validate the selected branch before returning:

- Clarification: each extraction field has a disposition and every material unknown has a focused question or confirmation risk. Return the three clarification sections.
- Drafting: the full output is present, every requirement traces through the Q/A/conclusion table, and all Business Requirements Rules hold.
