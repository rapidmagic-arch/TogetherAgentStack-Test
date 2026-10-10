# Task `124b59-T0001` — `Dry-run hello.txt implementation and end-to-end Lifecycle exercise`

## Purpose

Produce a single observable artifact `project-<WORK-ID>/hello.txt` on branch `impl/<WORK-ID>` whose content equals exactly `hello together agents`, then carry the Work through Design, Implementation, Review, Priority Refresh, and Final Review against this Task's Conditions and Verification criteria, so that the Repository's Lifecycle mechanics are exercised once end to end.

## In Scope

- Authoring the minimal Design that fixes the file path and the literal expected content for this artifact.
- Creating `project-<WORK-ID>/hello.txt` under branch `impl/<WORK-ID>` with the literal content `hello together agents`.
- Recording the resulting Commit SHA in Work Canonical as the active implementation commit.
- Submitting the implementation result for Review against `review_base_commit..reviewed_commit`.
- Updating `STATUS.yaml` and `TASK-INDEX.yaml` through Priority Refresh and Final Review stages.

## Out of Scope

- Any product feature development unrelated to the Lifecycle verification.
- Activation of Cron, Watcher, automated Writer, Kanban as canonical replacement, Webhook, or any adapter program.
- Any change to the upstream `TogetherAgentStack` template repository.
- Creation of `integrate/<WORK-ID>` or any Final Integration PR before the user explicitly approves closure.

## Conditions

- Branch `work/<WORK-ID>`, `design/<WORK-ID>`, `impl/<WORK-ID>` all start from base main Commit `16f8e619472e434468e2b305eaddb44012dce2ad` and this equality is verified before any commit is recorded in Work Canonical.
- The file `project-<WORK-ID>/hello.txt` exists on branch `impl/<WORK-ID>` after Implementation.
- The byte-equal content of that file is exactly the string `hello together agents` with no trailing whitespace, no leading whitespace, and no extra newline beyond the single terminating newline that is required by POSIX text files.

## Design References

- Minimal Design Commit authored on branch `design/<WORK-ID>` for this Work. The Design records the literal expected content and the file path; method changes within that scope are at the Implementer's discretion.

## Base Commit

`16f8e619472e434468e2b305eaddb44012dce2ad` (Task input baseline commit; the Review Base Commit is recorded separately at Result submission time).

## Expected Result

A single Commit on branch `impl/<WORK-ID>` that adds the file `project-<WORK-ID>/hello.txt` whose content is exactly `hello together agents\n`, with the Commit SHA recorded in Work Canonical as `active_impl_commit`.

## Verification

- A literal byte comparison against the expected content `hello together agents\n` is run against the file on branch `impl/<WORK-ID>` and the comparison output is recorded as Verification evidence.
- The Work Canonical `STATUS.yaml` field `active_impl_commit` is set to the exact Commit SHA that introduced it.
- The Reviewer judges PASS only against the explicit `review_base_commit..reviewed_commit` range, not against the current PR Head.

## Review Evidence

- Pull Request: NOT_APPLICABLE
- Review Base Commit: `16f8e619472e434468e2b305eaddb44012dce2ad` (equals Task Base Commit; the range contains exactly 1 commit, see notes below)
- Reviewed Commit: `b7b547eaff56562bb1c611c4a3cd1254905df117`
- Review Result: `PASS`
- Review Reference: REVIEWER-verified at work HEAD `a7b3dc815b336f7d117bda2636591feb8bd77cec` (this Work's Reviewer identity equals the same Git/Hermes identity that authored the Implementation commit; per `rules/contracts/git-review.yaml` `identity_boundary`, the PASS judgement is recorded here as Role-based evidence and is NOT treated as independent external reviewer approval). Diff range `16f8e619..b7b547e` contains exactly one commit touching a single file: `project-261010-workflow-dryrun-124b59/hello.txt`. Reviewer pulled the file blob from `b7b547e` (`git show b7b547e:project-261010-workflow-dryrun-124b59/hello.txt`) and confirmed: 22 bytes; sha256 `353039bcb4c34b9b65fbef9a3a9cc81f5cc2f0f759b2e9317503bd41dbb499c1`; trailing byte = LF; no CRLF (`grep -q $'
'`); no UTF-8 BOM (first 3 bytes = `hel`); no trailing whitespace (`grep -qE ' $'`); byte-equal to literal `hello together agents\n` (`diff -q` clean).

## Open Issues

- none

## Notes

This Task exists solely to exercise the Lifecycle. Process conversation belongs in events/issues. GitHub PR is review evidence, while Task completion remains recorded in TASK-INDEX and SUMMARY after PASS Review.

Range reasoning: The Implementation introduced a single commit `b7b547eaff56562bb1c611c4a3cd1254905df117` on top of base main `16f8e619472e434468e2b305eaddb44012dce2ad`. `git rev-list --count 16f8e619..b7b547e` returns 1, so the entire Task change range equals the Task Base Commit..Implementation Commit and the Review Base Commit naturally equals the Task Base Commit.