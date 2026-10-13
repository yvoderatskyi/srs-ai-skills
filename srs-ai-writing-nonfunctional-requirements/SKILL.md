---
name: srs-ai-writing-nonfunctional-requirements
description: Use when writing or checking measurable nonfunctional requirements, NFR thresholds, quality attributes, constraints, SLAs, or SLOs
---

# Writing Nonfunctional Requirements

Use this skill to turn approved goals, constraints, risks, operating context, and usage expectations into measurable nonfunctional requirements. Do not accept vague quality words as requirements.
Keep the trace chain visible from goal, constraint, or risk to each NFR and verification method.

## Material Gaps

When material ambiguity or conflicting terminology blocks this artifact, use `grill-with-docs` for the interview. Read `srs-ai-resolving-requirements-gaps` for the requirements ledger and handoff rules alongside it. Pass existing gap IDs, evidence, and affected artifact IDs; reuse resolved answers. After the interview, resume this skill's output and quality gate. Sufficient inputs proceed directly; persisted records supplement the response format below.

## Required Inputs

Use available success criteria, business goals, constraints, risks, compliance notes, architecture limits, use-case volumes, operating environments, stakeholder statements, and approved assumption IDs/references. Use the evidence policy below for missing or unconfirmed inputs.

## Output Format

Group NFRs by quality category or by the project's existing structure.

| NFR ID | Status | Quality category | Requirement | Threshold/metric | Operating context/environment | Source link | Verification method | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |

## Evidence and Status

Account for each supplied quality statement as an NFR row or an open issue with a reason. Use these statuses:

- `confirmed`: the source, threshold, operating context, and verification method are supported by confirmed input or an explicitly approved assumption. Cite evidence for the numeric target and context as well as the quality goal; a request for “fast” supports the goal, not a latency target.
- `provisional`: any required field is missing, inferred, or awaiting confirmation. Put `Missing - open issue OI-###` in unknown fields. Label proposed values as assumptions in Notes and link the confirmation question.

Record each open issue with its ID, affected NFR/field, missing decision, and source or stakeholder needed to resolve it. Retain provisional rows for review; promote them only when their evidence is complete.

## NFR Rules

- Use stable NFR IDs, such as `NFR-001`, `NFR-002`, or category-prefixed IDs when already established.
- Assign a quality category to every NFR, such as performance, security, availability, usability, privacy, compliance, interoperability, maintainability, observability, recoverability, or scalability.
- For confirmed NFRs, include a measurable threshold. The threshold must define pass/fail using a metric, limit, percentile, time window, volume, rate, score, standard, or audit criterion.
- For confirmed NFRs, state the operating context/environment where the threshold applies, including relevant users, load, device, network, deployment, region, vendor, regulatory boundary, or peak/normal condition.
- For confirmed NFRs, give a source link to a success criterion, constraint, risk, use-case context, business goal, stakeholder statement, or approved assumption ID/reference.
- For confirmed NFRs, define a verification method that can prove the threshold, such as load test, security test, penetration test, accessibility audit, failover drill, recovery exercise, monitoring review, log inspection, compliance audit, or contract test.

## Measurability Check

Revise or flag any NFR that relies on vague wording such as `fast`, `secure`, `reliable`, `scalable`, `robust`, `intuitive`, `easy`, `usable`, `high availability`, or `appropriate` without a metric and context.

Prefer this shape:

```text
Under <operating context>, the system shall meet <threshold/metric> because of <source link>; verify by <method>.
```

## Quality Gate

Before returning, account for every supplied quality statement. Check each row against NFR Rules and Evidence and Status: confirmed rows satisfy every field rule; provisional rows identify each unresolved field and link a recorded open issue. Return unresolved decisions alongside the table.
