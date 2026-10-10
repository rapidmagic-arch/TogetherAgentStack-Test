# Design Item `124b59-0001` — `hello.txt artifact contract`

## Purpose

Fix the path and exact byte content of the single observable artifact required by Task `124b59-T0001`, so that the Repository Lifecycle end-to-end exercise has a verifiable, non-ambiguous outcome.

## Scope

### In

- Selection of artifact path: `project-<WORK-ID>/hello.txt` on branch `impl/<WORK-ID>`.
- Selection of literal artifact content: the string `hello together agents` followed by exactly one LF (`\n`) byte and nothing else.
- Selection of verification method: byte-equal comparison of the on-branch file against the literal bytes `hello together agents\n`.

### Out

- Any additional metadata files, build configuration, or tests beyond the byte comparison.
- Any expansion of product scope beyond the Lifecycle verification.
- Method-level choices about how the file is produced (editor, redirection, programmatic generation); those remain at the Implementer's discretion within the constraints of this Design.

## Current Problem

Task `124b59-T0001` requires an observable artifact whose exact path and content are otherwise undefined. Without a Design decision, the Lifecycle exercise cannot reach a deterministic PASS/REWORK judgement.

## Required Outcome

After Implementation, branch `impl/<WORK-ID>` contains the file `project-<WORK-ID>/hello.txt` whose bytes equal exactly `hello together agents\n`. The Reviewer can confirm PASS by running a byte-equal comparison against that literal.

## Constraints

- The file MUST use LF line endings only; CRLF or mixed endings MUST be a REWORK.
- The file MUST NOT include a UTF-8 BOM, trailing whitespace, or any character before or after the literal.
- The Implementation MUST land on branch `impl/<WORK-ID>` whose tip is recorded in Work Canonical as `active_impl_commit`.

## Decision

Implementer MUST create the file `project-<WORK-ID>/hello.txt` on branch `impl/<WORK-ID>` and the file content MUST be exactly the literal string `hello together agents` followed by a single terminating newline (LF only, no CRLF).

## Interfaces / Data / State

- Input: the literal bytes `hello together agents\n` (single source of truth for expected content).
- Output: a single file at the path above, on branch `impl/<WORK-ID>`.
- State transitions observed: file absent on `impl/<WORK-ID>` before Implementation, file present with exact bytes after the Implementation commit lands.

## Verification Criteria

- A byte-equal comparison between the on-branch file and the literal bytes `hello together agents\n` returns success.
- The Commit that introduced the file is recorded in `work/<WORK-ID>/STATUS.yaml` as `active_impl_commit`.
- The Reviewer PASS judgement is anchored to `review_base_commit..reviewed_commit` and not to the PR Head alone.

## Open Questions

- none

## References Used

- none

## Change Notes

- Linked to Task `124b59-T0001`. The TASK.md Conditions, Verification, and Expected Result reflect this Design verbatim.

## Rationale

This Task exists solely to exercise the Repository Lifecycle end to end. The artifact is the smallest observable result that can verify the Lifecycle mechanics while remaining trivially verifiable by byte comparison. The choice of path (`project-<WORK-ID>/hello.txt`) and the literal content (`hello together agents`) are fixed by this Design; method-level choices about how the file is produced (editor, redirection, programmatic generation) remain at the Implementer's discretion within the constraints above.

## Scope Boundary

- IN: path selection, literal content selection, verification method (byte comparison), required single trailing LF.
- OUT: any additional metadata files, build configuration, tests beyond the byte comparison, product-feature expansion.

## Verification Approach

Reviewer MUST run a byte-equal comparison against the literal bytes `hello together agents\n` against the file `project-<WORK-ID>/hello.txt` checked out from the reviewed Commit on branch `impl/<WORK-ID>`. Any deviation in whitespace, line endings, or surrounding characters MUST yield REWORK or DESIGN_ISSUE depending on whether the deviation is fixable inside this Task's scope.