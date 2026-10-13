# Pressure Scenarios

These RED scenarios define failures this skill must prevent before it is used to draft business requirements.

## RED Scenario 1: Founder gives one vague phrase

Prompt: "Our founder says: 'Make returns less painful.' Write the business requirements."

Expected unskilled failure:
- Converts the phrase directly into a polished requirements list.
- Invents the business problem, customer segment, operating goals, and workflow.
- Omits questions, stakeholder uncertainty, and measurable success criteria.

Required correction in skill:
- Extract what is known and unknown before drafting.
- Ask focused clarification questions.
- Mark all invented details as assumptions.

## RED Scenario 2: Stakeholder access is limited

Prompt: "The sponsor is unavailable until next week. Infer the requirements now from sales notes."

Expected unskilled failure:
- Treats weak notes as confirmed stakeholder intent.
- Fails to separate facts, assumptions, risks, and open questions.
- Produces requirements that cannot be validated later.

Required correction in skill:
- Use available sources only as provisional evidence.
- Build a Q/A/conclusion table that shows uncertainty.
- Record confirmation risks and measurable success criteria.

## RED Scenario 3: Agent invents goals instead of asking

Prompt: "We need requirements for an AI onboarding assistant. You know what goals matter."

Expected unskilled failure:
- Invents goals such as conversion lift, support deflection, or activation rate.
- Hides assumptions inside confident requirements language.
- Does not ask which stakeholders define success.

Required correction in skill:
- Ask focused questions about stakeholders, goals, constraints, and risks.
- Label any proposed goals as assumptions until confirmed.
- Produce conclusions only from stated answers or explicit assumptions.

## GREEN Verification Targets

- Skill requires extracting business problem, stakeholders, goals, constraints, success criteria, assumptions, and risks.
- Skill requires focused clarification questions before requirements.
- Skill requires Q/A/conclusion tables and measurable success criteria.
- Skill requires marking invented details as assumptions.
- Skill blocks draft requirements from vague input when material fields are missing unless evidence resolves material gaps or provisional requirements are explicitly authorized.

## Regression Scenario: Clarification and drafting branches

Prompt: "We need better onboarding. The sponsor is unavailable and goals are unknown."

Pass criteria:
- Without provisional drafting authorization, return only the three clarification sections.
- Every extraction field is known, unknown, or not applicable with a reason.
- If the user subsequently authorizes a provisional draft, return the full format with unresolved success criteria linked to questions.
- A partial answer that leaves material gaps does not automatically unlock drafting.

## Regression Scenario: Persist answers between clarification rounds

Prompt: "Help define our onboarding goals; ask me as needed."

Pass criteria:
- Use the gap-resolution skill for material unknowns; rounds follow upstream prerequisite ordering.
- Save answered questions before asking dependent questions, while preserving the clarification response sections.
- Once material gaps resolve, populate the Q/A/conclusion table from those records without repeating the interview.
- A resolved answer does not automatically approve the business requirements.
