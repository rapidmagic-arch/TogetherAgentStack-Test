# Design Item `46fdf8-0001` — `writer-test.txt artifact contract`

## Purpose

Fix the path and exact byte content of the single observable artifact required by Task `46fdf8-T0001`, so that the Repository Lifecycle's DESIGNER Handoff — when executed through the `workspace-tas-writer` Hermes Skill — can be verified end to end.

## Scope

### In

- Selection of artifact path: `project-<WORK-ID>/writer-test.txt` on branch `impl/<WORK-ID>`.
- Selection of literal artifact content: the string `writer handoff test` followed by exactly one LF (`\n`) byte and nothing else.
- Selection of verification method: byte-equal comparison of the on-branch file against the literal bytes `writer handoff test\n`.

### Out

- Any additional metadata files, build configuration, or tests beyond the byte comparison.
- Any expansion of product scope beyond the Writer Skill verification.
- Method-level choices about how the file is produced; those remain at the Implementer's discretion within the constraints of this Design.

## Current Problem

Without a Design decision, the Implementer cannot deterministically match the expected artifact, and the Writer Skill's Handoff record would reference an under-specified Design.

## Required Outcome

After Implementation, branch `impl/<WORK-ID>` contains the file `project-<WORK-ID>/writer-test.txt` whose bytes equal exactly `writer handoff test\n`. Verification is byte-equal comparison.

## Constraints

- The file MUST use LF line endings only; CRLF or mixed endings MUST be a REWORK.
- The file MUST NOT include a UTF-8 BOM, trailing whitespace, or any character before or after the literal.
- The Implementation MUST land on branch `impl/<WORK-ID>` whose tip is recorded in Work Canonical as `active_impl_commit`.

## Decision

Implementer MUST create the file `project-<WORK-ID>/writer-test.txt` on branch `impl/<WORK-ID>` containing exactly the bytes `writer handoff test\n` and nothing else. Verification is byte-equal comparison. Method-level choices about how to author the file remain at the Implementer's discretion within these constraints.

## Interfaces / Data / State

- Input: the literal bytes `writer handoff test\n` (single source of truth for expected content).
- Output: a single file at the path above, on branch `impl/<WORK-ID>`.
- State transitions observed: file absent on `impl/<WORK-ID>` before Implementation, file present with exact bytes after the Implementation commit lands.

## Verification Criteria

- A byte-equal comparison between the on-branch file and the literal bytes `writer handoff test\n` returns success.
- The Commit that introduced the file is recorded in `work/<WORK-ID>/STATUS.yaml` as `active_impl_commit`.

## Open Questions

- none

## References Used

- none

## Change Notes

- Linked to Task `46fdf8-T0001`. The TASK.md Conditions, Verification, and Expected Result reflect this Design verbatim.