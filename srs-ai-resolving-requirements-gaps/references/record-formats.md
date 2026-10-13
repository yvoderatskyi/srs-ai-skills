# Record Formats

## Locations and Ownership

Write into the user's project workspace, not the installed skill directory. Reuse established locations and formats. Otherwise use `docs/requirements/context-ledger.md` and root `GLOSSARY.md`. If root `GLOSSARY-MAP.md` exists, follow its context-specific glossary locations; clarify an ambiguous context before changing its vocabulary. Create files only when there is content.

The orchestrator owns the overall ledger; this skill updates it during interviews. A standalone requirements skill uses the same records without starting the full SRS workflow. Preserve unrelated entries and existing IDs. Missing write access changes the delivery to explicit unsaved records, not a claim of persistence.

## Context Ledger

Retain the existing fields: `source`, `decision`, `ids`, `status`, `risk`, `artifact/version`, and `approval evidence`. Add these fields to interview entries using the project's existing table or record structure:

| Field | Meaning |
| --- | --- |
| `record ID` | Stable question/decision ID; reuse an existing gap ID or allocate `Q-001` onward |
| `question` | Decision being resolved |
| `prerequisites` | IDs that must resolve before this question can be answered, or `None` |
| `resolution` | `open`, `resolved`, or `deferred` |
| `affected artifacts` | Artifact IDs/sections influenced by the answer |
| `follow-up` | For unresolved decisions: impact, blocking status, and stakeholder/source needed |

Record the answer in `decision`, with evidence in `source`. Preserve exact numeric defaults, units, conditions, exceptions, and exclusions. Recommendations and inferred answers remain labeled assumptions. Historical answers must remain recoverable when superseded; record the new evidence and affected versions.

Resolution and approval are separate: an answered question may be `resolved` while its resulting requirement is `proposed`. Use `approved` only for explicit acceptance by the user or an authorized reviewer within the recorded scope; keep reviewer, source, and version in `approval evidence`. Silence and drafting authorization are not acceptance. On revision, mark affected approved rows `changed` and identify downstream links.

For a new ledger, Markdown records headed by record ID are sufficient; use the field names above rather than a very wide table. Keep the ledger's established format when one exists.

## Canonical Glossary

Use the installed `domain-modeling` skill's `GLOSSARY-FORMAT.md` for canonical vocabulary. Keep source evidence and term-to-artifact links in the requirements ledger, linking each settled term to its glossary location.

Save settled domain meanings with a linked source ledger record. Keep proposals and unresolved definitions in the ledger until resolved. The glossary contains vocabulary; behavior, thresholds, implementation choices, and interview notes belong in requirements or decision records.

When later data modeling needs a glossary section, link the canonical glossary and relevant terms instead of maintaining a second authoritative copy. In a standalone response without files, provide the glossary inline and label its persistence status.
