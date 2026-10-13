# Pressure Scenarios

Subagent execution was not available without explicit delegation permission in this session, so these RED scenarios document the local baseline risks the skill is designed to prevent.

## RED Scenario 1: Presales speed pressure

Prompt: "A founder says: 'Make a clinic reminder app so fewer patients miss appointments.' Create a technical specification quickly."

Expected unskilled failure:
- Generates a full SRS immediately.
- Invents channels, integrations, compliance constraints, and user roles.
- Does not separate assumptions from confirmed stakeholder input.

Required correction in skill:
- Forbid one-pass SRS generation.
- Start with interview questions, success criteria, and assumptions.

## RED Scenario 2: Artifact consistency pressure

Prompt: "Use AI to create FRs, use cases, a data model, and NFRs for the same system."

Expected unskilled failure:
- Produces each artifact independently.
- Uses inconsistent names and IDs.
- Does not link FR -> UC -> entity -> NFR.

Required correction in skill:
- Maintain a context ledger.
- Require traceability IDs in every artifact.

## RED Scenario 3: Missing stakeholder access

Prompt: "We cannot talk to the stakeholder. Simulate the stakeholder and finalize requirements."

Expected unskilled failure:
- Treats simulated stakeholder answers as real requirements.
- Fails to label uncertainty and confirmation needs.

Required correction in skill:
- Allow cognitive simulation only as preparation or training.
- Mark simulated content as assumptions and require confirmation before final SRS.

## RED Scenario 4: Step routing pressure

Prompt: "I already have goals and context. Write the functional requirements only."

Expected unskilled failure:
- Generates unrelated SRS sections.
- Does not route to step-specific guidance.
- Drops approved context and traceability links.

Required correction in skill:
- Route this request to `srs-ai-writing-functional-requirements`.
- Keep the context ledger as the shared contract.

## GREEN Verification Targets

- Skill description triggers on vague ideas, AI-assisted SRS, FR/NFR, use cases, diagrams, data models, and traceability.
- Skill body requires building and reviewing one artifact at a time before final assembly.
- Workflow has seven ordered artifact steps.
- Skill requires uncertainty checks, context passing, trace IDs, and human analyst verification.

## Regression Scenario: Approval, revisions, and final assembly

Prompt: "Draft an SRS from these mixed approved and proposed artifacts. We approved context v1, but v2 changes the boundary."

Pass criteria:
- Approval evidence identifies the reviewer and accepted version; context v2 and affected downstream rows are changed/proposed.
- Unaffected approvals remain valid and provisional work retains its status.
- The inventory accounts for every artifact; traceability gaps and contradictions appear in the review report.
- The output remains a draft until required artifacts, blocking issues, and assembled-version approval satisfy the final gate.

## Regression Scenario: Interview handoff within the workflow

Prompt: "Continue from our saved requirements ledger. The last session resolved the reminder dispatch target, but the retention owner is unavailable. Draft the NFR section provisionally."

Pass criteria:
- Reuse the resolved target and source ID without interviewing again.
- Use the gap-resolution skill for the outstanding retention decision and record an explicit deferral with its impact.
- Return to NFR generation with the target unchanged and retention provisional.
- Update the same project ledger rather than creating a parallel interview record or restarting business elicitation.
