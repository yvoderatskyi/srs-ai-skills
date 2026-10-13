---
name: srs-ai-writing-nonfunctional-requirements
description: Use when specifying or auditing measurable nonfunctional requirements (NFRs), quality thresholds, operating contexts, and verification methods
---

# Writing Nonfunctional Requirements

Turn approved goals, success criteria, constraints, risks, and operating context into measurable nonfunctional requirements. Keep the trace chain visible from upstream source to each NFR threshold and verification method.

**Material gaps:** When material ambiguity or conflicting terms block this artifact, invoke `grill-with-docs` alongside `srs-ai-resolving-requirements-gaps` to update the context ledger (pass gap/artifact IDs and evidence; reuse resolved answers; resume here after). Sufficient inputs proceed directly; persisted records supplement the response format below.

## Output Format & Evidence Status

Group NFRs by quality category (performance, security, availability, usability, privacy, compliance, interoperability, maintainability, observability, recoverability, scalability) or the project's established structure:

| NFR ID | Status | Quality category | Requirement | Threshold/metric | Operating context/environment | Source link | Verification method | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |

Account for every supplied quality statement as an NFR row or an open issue with a reason:

- `confirmed`: Source, measurable threshold, operating context, and verification method are backed by confirmed input or an explicitly approved assumption ID. Cite evidence for the numeric target and context separately from the quality goal (a request for "fast" supports the goal, while the latency target remains `provisional` until confirmed).
- `provisional`: Any required field is missing, inferred, or awaiting confirmation. Write `Missing - open issue OI-###` in unknown fields, label proposed values as assumptions in `Notes`, and link the confirmation question.

Record each open issue (`OI-###`) alongside the table with its affected NFR/field, missing decision, and the source or stakeholder needed to resolve it.

## NFR & Measurability Rules

- **Stable IDs**: Use persistent IDs (`NFR-001`, `NFR-002`, or established category prefixes).
- **Measurable threshold**: Convert vague quality words (`fast`, `secure`, `reliable`, `scalable`, `robust`, `intuitive`, `easy`, `usable`, `high availability`, `appropriate`) into pass/fail metrics using limits, percentiles, time windows, volumes, rates, scores, standards, or audit criteria.
- **Operating context**: State the users, load, device, network, deployment, region, vendor, regulatory boundary, or peak/normal condition where the threshold applies.
- **Source link**: Cite a success criterion, constraint, risk, use-case context, business goal, stakeholder statement, or approved assumption ID.
- **Verification method**: Specify a concrete proof method (load test, penetration test, accessibility audit, failover drill, recovery exercise, monitoring review, log inspection, compliance audit, or contract test).
- **Target phrasing**:
  ```text
  Under <operating context>, the system shall meet <threshold/metric> because of <source link>; verify by <method>.
  ```

## Quality Gate

Before returning, verify that every supplied quality statement is accounted for, every `confirmed` row satisfies all NFR & Measurability Rules with evidence-backed fields, and every `provisional` row marks unknown fields with `Missing - open issue OI-###`, labels assumptions in `Notes`, and lists its open issue alongside the table.
