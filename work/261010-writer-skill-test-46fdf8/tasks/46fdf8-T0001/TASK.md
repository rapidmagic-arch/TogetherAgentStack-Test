# Task `46fdf8-T0001` — `Writer Skill first test — DESIGNER Handoff recorded via Writer procedure`

## Purpose

This Task verifies that the `workspace-tas-writer` Hermes Skill, when followed step by step, produces a complete and consistent DESIGNER Handoff record in Work Canonical and pushes it to the remote without losing data.

## In Scope

- Authoring a minimal Design Item on `design/<WORK-ID>` that fixes the path and the exact byte content of the final artifact.
- Following the Writer Skill's documented 13-step procedure to record the DESIGNER Handoff in `work/<WORK-ID>/STATUS.yaml` and `TASK-INDEX.yaml`.
- Committing and pushing the Handoff to the remote work branch.
- Verifying that the remote work HEAD equals the local Handoff commit SHA.

## Out of Scope

- Implementation, Review, Final Review, Integration stages.
- Activating Watcher / Cron / Kanban / Webhook / adapter.
- Modifying the upstream TogetherAgentStack Template or the Writer Skill's body content.
- Any CLOSED / COMPLETE / INCOMPLETE transition (these are HUMAN-exclusive per `roles.yaml`).

## Conditions

- The three standard work branches `work/<WORK-ID>`, `design/<WORK-ID>`, `impl/<WORK-ID>` all start from base main Commit `5e8204221d387310bb7ad17e3c0e337a029f662c`.
- A Design Item exists on `design/<WORK-ID>` and the Design Commit SHA is recorded in `STATUS.yaml` as `active_design_commit`.
- `STATUS.yaml`'s `next_actor` is `IMPLEMENTER` and `last_actor` is `DESIGNER` after the Handoff.
- The remote `work/<WORK-ID>` HEAD equals the local Handoff commit SHA after Push.

## Design References

- Design Item to be authored on `design/<WORK-ID>` for this Work. The Design Item only fixes the literal artifact path and content; implementation method is at Implementer's discretion.

## Base Commit

`5e8204221d387310bb7ad17e3c0e337a029f662c` (Task input baseline commit; the Review Base Commit will be recorded separately at Result submission time, but this Work does not proceed past DESIGNER Handoff).

## Expected Result

A single Handoff commit on `work/<WORK-ID>` that updates `STATUS.yaml` and `TASK-INDEX.yaml` and references the Design Commit on `design/<WORK-ID>`. After Push, the remote `work/<WORK-ID>` HEAD equals this commit's SHA and `git ls-remote origin work/<WORK-ID>` shows the same SHA.

## Verification

- `git show <handoff-commit>:work/<WORK-ID>/STATUS.yaml` shows `work_state=PROGRESS`, `next_actor=IMPLEMENTER`, `last_actor=DESIGNER`, `active_design_commit=<Design Commit SHA>`.
- `git show <handoff-commit>:work/<WORK-ID>/TASK-INDEX.yaml` shows the registered task and the priority ordering.
- `git ls-remote origin work/<WORK-ID>` returns the same SHA as `git rev-parse work/<WORK-ID>`.

## Review Evidence

- Pull Request: NOT_APPLICABLE
- Review Base Commit: UNKNOWN (this Work does not reach Review in this round)
- Reviewed Commit: UNKNOWN
- Review Result: UNKNOWN
- Review Reference: <not applicable for this Work>

## Open Issues

- none

## Notes

This Task is a Writer-Skill verification, not a product Work. The Handoff record itself is the verification target.