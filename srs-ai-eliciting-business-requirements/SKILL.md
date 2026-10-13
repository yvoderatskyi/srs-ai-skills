---
name: srs-ai-eliciting-business-requirements
description: Use when eliciting business problems, stakeholder goals, constraints, assumptions, or measurable success criteria before system requirements
---

# Eliciting Business Requirements

Turn uncertain business input into validated business requirements and keep the trace chain visible from question to conclusion to requirement.

**Material gaps:** When material ambiguity or conflicting terms block this artifact, invoke `grill-with-docs` alongside `srs-ai-resolving-requirements-gaps` to update the context ledger (pass gap/artifact IDs and evidence; reuse resolved answers; resume here after). Sufficient inputs proceed directly; persisted records supplement the response format below.

## Extraction & Branch Selection

Extract and maintain these fields from available evidence first:

| Field | What to capture |
| --- | --- |
| Business problem | Pain, opportunity, or decision the work addresses (who feels it today) |
| Stakeholders | Approvers, users, operators, affected teams, and unavailable groups |
| Goals | Desired business outcomes (cost, revenue, risk, speed, quality, satisfaction, compliance) |
| Constraints | Fixed deadlines, systems, policies, budgets, legal limits, and operating boundaries |
| Success criteria | Measurable outcomes defining whether the business goal was achieved |
| Assumptions | Any invented, inferred, simulated, or unconfirmed detail |
| Risks | Ambiguity, missing stakeholder access, contradictory evidence, feasibility, or validation gaps |

Select one branch after extraction:

- **Clarification:** Material inputs remain missing or uncertain and provisional drafting is not authorized. Return only `1. Known Context`, `2. Focused Questions`, and `3. Assumptions and Risks`. Account for every extraction field as `known`, `unknown`, or `not applicable` with a reason; ask small question sets covering material unknowns.
- **Drafting:** Available evidence resolves material gaps, or the user explicitly authorized provisional requirements. Produce all six output sections below. Mark inferred answers and unresolved decisions as assumptions; identify unavailable stakeholders and the confirmation needed. Authorization to draft leaves assumptions unconfirmed.

## Output Format (Drafting Branch)

Produce these sections in order (write `None` for Focused Questions when supplied evidence is sufficient):

1. **Known Context**
2. **Focused Questions**
3. **Q/A/Conclusion Table**

| ID | Question | Answer or assumption | Conclusion | Confidence | Follow-up |
| --- | --- | --- | --- | --- | --- |

Distinguish confirmed stakeholder input from labeled assumptions in `Answer or assumption`. Every conclusion must trace to an answer, source note, or labeled assumption.

4. **Draft Business Requirements**

| ID | Requirement | Source conclusion | Priority | Uncertainty |
| --- | --- | --- | --- | --- |

- State business-level outcomes, policies, decisions, constraints, and capabilities.
- Link every requirement to a conclusion ID from the Q/A/Conclusion Table.
- Label unconfirmed goals as assumptions and preserve uncertainty explicitly in `Uncertainty`.

5. **Measurable Success Criteria**

| ID | Metric | Target | Timeframe | Source or assumption |
| --- | --- | --- | --- | --- |

- Populate metric, target, timeframe, and source or assumption for every row. When a field is unresolved, link a question ID and mark the criterion `provisional`.

6. **Assumptions and Risks**

## Quality Gate

Validate the selected branch before returning:

- **Clarification:** Every extraction field has a disposition (`known`, `unknown`, or `not applicable` with reason), every material unknown has a focused question or confirmation risk, and only the three clarification sections are returned.
- **Drafting:** All six sections are present, every requirement traces through a conclusion ID to its source or labeled assumption, and every success criterion has all four fields or a linked question marking it provisional.
