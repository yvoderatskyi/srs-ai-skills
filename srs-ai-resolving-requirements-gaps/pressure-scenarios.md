# Pressure Scenarios

These are behavioral evaluation cases, not runtime references or evidence of executed tests. Run each in an isolated project workspace with the named calling skill, this adapter, and all three upstream skills installed. Inspect the conversation and saved artifacts; evaluate outcomes rather than matching instruction wording.

## 1. Discoverable facts and intended behavior

Fixture: existing FR-001 requires email reminders; code currently sends SMS. The user asks to clarify notification requirements.

Pass: inspect both sources, describe current versus intended behavior, and ask which behavior is desired. Do not ask the user to identify the current code behavior or treat code as approval.

## 2. Dependent questions and partial answers

Prompt: "We need retention rules. Decide which records are retained and how long."

After the first round, answer only which records are covered.

Pass: use upstream rounds of ready questions with IDs and recommendations. Retention periods dependent on record scope wait for scope resolution. Persist the answered decision immediately; keep unanswered questions open. Recommendations do not become answers.

## 3. Sufficient inputs

Fixture: a complete, sourced, approved FR list and context model; request use-case modeling with no conflicting terms.

Pass: the calling skill produces the requested artifact without starting an interview or creating empty glossary/ADR files.

## 4. Conflicting terminology

Fixture: `GLOSSARY.md` defines "dispatch" as provider acceptance. User uses "dispatch" to mean receipt on the handset.

Pass: surface the conflict with a concrete example. Keep unresolved meaning in the ledger. After the user settles it, update the canonical glossary that round, preserve the source, and identify affected requirements. Later data modeling links this glossary rather than creating a second authoritative definition.

## 5. Exact threshold through handoff

Prompt: "Write dispatch-latency NFRs; we haven't agreed on a target."

Answer: "p95 <= 60 seconds from scheduled send time to provider acceptance at 10,000 appointments/hour; exclude patient delivery latency. Verify with a load test."

Pass: ledger, NFR row, and later SRS preserve percentile, inequality, units, endpoints, load, exclusion, and method. Cite the answer's stable ID. No substitution with "fast" or a weaker average. Resolving the answer does not automatically approve the artifact.

## 6. Unavailable stakeholder and provisional work

Prompt: "The privacy owner is unavailable. Draft provisionally; we do not know the retention period."

Pass: explicitly defer the decision with blocking impact and needed stakeholder. Preserve the unknown period, finish the interview with a deferred blocker, and return a provisional artifact under the caller's rules. Neither invent a confirmed period nor continue asking the same unavailable question.

## 7. Resume after an answered round

Fixture: a saved ledger with Q-001 resolved, Q-002 open and dependent on Q-001, plus an existing glossary. Start a new session asking to continue the artifact.

Pass: read the records, reuse IDs, ask Q-002 without repeating Q-001, and save the next answer before continuing. Report actual saved paths. Existing unrelated entries remain intact.

## 8. Ordinary decisions and selective ADRs

Fixture: one settled display label and one settled external retention obligation whose reversal is costly, whose rationale is nonobvious, and for which competing alternatives were discussed.

Pass: save both decisions in the ledger. Create an ADR only for the latter, with alternatives, consequences, source IDs, and accurate approval status. Zero qualifying decisions produces zero ADR files.

## 9. Changed upstream approval

Fixture: context v1 and FR-001 are approved; user changes the system boundary for context v2. FR-002 is independent.

Pass: retain earlier evidence, mark affected approved rows changed, identify downstream links, and revise the affected scope. Preserve FR-002's approval. The new answer is not blanket approval of context v2 or revised FR-001.

## 10. No file writes

Fixture: read-only or chat-only session.

Pass: return ledger/glossary/ADR content as applicable, state it was not saved, and retain the caller's provisional/approval semantics. Never claim a file exists because its content was drafted.

## 11. Multi-context glossary

Fixture: root `GLOSSARY-MAP.md` routes billing and scheduling vocabulary to different directories; both contain a term called "account".

Pass: select the relevant context from evidence or ask when ambiguous. Update only that context's glossary, without creating a competing root definition.

## 12. Standalone invocation and scoped completion

Prompt: "Use the NFR skill to resolve this one timeout requirement."

Pass: use shared records without starting the full seven-stage workflow. Once all material gaps are resolved or explicitly deferred and shared understanding is confirmed, return to NFR output and its gate. An explicit pause returns pending IDs rather than treating silence as resolution.

## 13. Dependency loading and invocation policy

Fixture: run once with all upstream skills installed and once with `domain-modeling` unavailable.

Pass: every material-gap interview in the selected workflow loads the `grill-with-docs` entrypoint and both dependencies, without bypassing the entrypoint, requesting repeated selection, or altering its installed invocation policy. Name loaded skills. Missing dependencies produce a clear report and installation guidance; ordinary clarification remains available without falsely claiming an upstream interview ran.

## 14. Shared understanding versus artifact approval

Fixture: all questions answered, but no shared-understanding confirmation yet.

Pass: apply upstream confirmation before handing back. Reuse an existing in-scope confirmation when present. Record that confirmation separately from approval of subsequently generated requirements.
