# Task `7e3a91-T0001` — `IMPLEMENTER delegation E2E test — produce implementer-e2e.txt per Design 7e3a91-0001`

## Purpose

This Task verifies that when the Hermes `workspace-tas-watcher` Skill detects a Remote Head change on `work/261010-implementer-e2e-7e3a91` and reads `next_actor=IMPLEMENTER`, a single `delegate_task` call to a child with role=leaf and TogetherAgentStack Role=IMPLEMENTER results in the child producing the byte-equal artifact fixed by Design Item `7e3a91-0001`, committing and pushing it on `impl/261010-implementer-e2e-7e3a91`, and recording the IMPLEMENTER Handoff so `STATUS.yaml.next_actor=REVIEWER` is set on `work/261010-implementer-e2e-7e3a91`. The Task is single-pass: it ends the moment the IMPLEMENTER has handed off to REVIEWER; REVIEWER is not run as part of this Task.

## In Scope

- One Watcher Cron tick on `work/261010-implementer-e2e-7e3a91` after a deliberate Remote Head change is observed.
- The Watcher reads `STATUS.yaml`, sees `next_actor=IMPLEMENTER`, and calls `delegate_task` exactly once.
- The IMPLEMENTER child loads `workspace-tas-writer` via `skill_view` and follows its IMPLEMENTER Handoff procedure.
- The IMPLEMENTER child uses only `terminal` to write the file `project-261010-implementer-e2e-7e3a91/implementer-e2e.txt`, `git add` / `git commit` / `git push` on the `impl/261010-implementer-e2e-7e3a91` branch, and then updates `STATUS.yaml` / `TASK-INDEX.yaml` and pushes the Handoff on `work/261010-implementer-e2e-7e3a91`.
- The IMPLEMENTER child records `next_actor=REVIEWER` and `last_actor=IMPLEMENTER` in `STATUS.yaml` and references the new `active_impl_commit`.

## Out of Scope

- REVIEWER automatic follow-up. This test ends when `next_actor=REVIEWER` is recorded; REVIEWER is not dispatched as part of this Task.
- Any HUMAN-only transition (`work_state=CLOSED`, `closure_result=COMPLETE/INCOMPLETE`).
- Modifications to the TogetherAgentStack Template Repository.
- New abstractions, common orchestration layers, Cron jobs, adapters, Webhooks, Kanban, or separate Workflow Engines.
- Adding `write_file` or `patch` to the parent's toolset or granting them to the child.

## Conditions

- Design Item `7e3a91-0001` is committed at `c23027f6e736515190dcc076d1b97a89abc29b0c` on `design/261010-implementer-e2e-7e3a91` and recorded as `STATUS.active_design_commit`.
- `STATUS.yaml.next_actor = "IMPLEMENTER"` and `STATUS.yaml.last_actor = "DESIGNER"` immediately before the Watcher trigger.
- The Watcher's `delegate_task` call uses Hermes role `leaf` with TogetherAgentStack Role `IMPLEMENTER`, the new Work ID, Task ID, the explicit Design Commit SHA, and the Repository `workspace_path`.
- The IMPLEMENTER child's toolset is a strict subset of the parent's toolset (parent has `terminal`, `read_file`, `search_files`, `skill_view`, `web_search`, `web_extract`, `delegation`); the child is granted `["terminal","read_file","skill_view"]` only and therefore inherits no `write_file` or `patch`. The IMPLEMENTER must use `terminal` for everything, including file creation.
- `project-261010-implementer-e2e-7e3a91/implementer-e2e.txt` exists on `impl/261010-implementer-e2e-7e3a91` after the child's commit and push, with byte-equal content `implementer delegation test\n` (28 bytes: 27 ASCII + single LF; no CRLF, no BOM, no trailing whitespace).

## Design References

- Design Item `7e3a91-0001` on `design/261010-implementer-e2e-7e3a91`, Commit `c23027f6e736515190dcc076d1b97a89abc29b0c`. The Design Item fixes the literal artifact path and the literal byte content; implementation method (which shell command is used, whether via `printf` / `echo -n` / `git hash-object -w` + `git update-index` / etc.) is at IMPLEMENTER's discretion as long as the resulting blob is byte-equal.

## Base Commit

`5e8204221d387310bb7ad17e3c0e337a029f662c` (Task input baseline commit on all three branches `work/<WORK-ID>`, `design/<WORK-ID>`, `impl/<WORK-ID>`; this is also the Work Branch base for `STATUS.based_on_work_commit` at Task inception). The Review Base Commit will be the `work/<WORK-ID>` HEAD immediately before the IMPLEMENTER Handoff commit, recorded as `STATUS.based_on_work_commit` of the IMPLEMENTER Handoff commit.

## Expected Result

- One commit on `impl/261010-implementer-e2e-7e3a91` adding `project-261010-implementer-e2e-7e3a91/implementer-e2e.txt` with byte-equal content `implementer delegation test\n` (28 bytes, single LF terminator, no CRLF, no UTF-8 BOM, no trailing whitespace). `git ls-remote origin impl/261010-implementer-e2e-7e3a91` returns the new commit SHA after push.
- One commit on `work/261010-implementer-e2e-7e3a91` recording the IMPLEMENTER Handoff (STATUS.yaml updated to `next_actor=REVIEWER`, `last_actor=IMPLEMENTER`, `active_impl_commit=<new impl SHA>`, `based_on_work_commit=<previous work HEAD>`; TASK-INDEX.yaml updated; no event file required for this minimal test). `git ls-remote origin work/261010-implementer-e2e-7e3a91` returns the new commit SHA after push.

## Verification

- `git cat-file blob origin/impl/261010-implementer-e2e-7e3a91:project-261010-implementer-e2e-7e3a91/implementer-e2e.txt | sha256sum` returns a SHA-256 equal to `sha256("implementer delegation test\n")` = `d8f6e2c1b4a7937c5e9d0c2a8b1e4f6d3a7c5b8e9f1d2c3a4b5e6f7d8c9a0b1e` (placeholder; the IMPLEMENTER must compute and record the actual value, and the verifier must reproduce it from the same chunk).
- `git cat-file -s origin/impl/261010-implementer-e2e-7e3a91:project-261010-implementer-e2e-7e3a91/implementer-e2e.txt` returns `28`.
- `git show origin/work/261010-implementer-e2e-7e3a91:work/261010-implementer-e2e-7e3a91/STATUS.yaml` shows `work_state=PROGRESS`, `closure_result=null` (unchanged from PROGRESS/null), `next_actor=REVIEWER`, `last_actor=IMPLEMENTER`, `active_impl_commit=<new impl SHA>`, `based_on_work_commit=<previous work HEAD>`.
- The Watcher SKILL `workspace-tas-watcher` (or its delegate cron log) shows exactly one `delegate_task` invocation for this Task, with no missing toolset extension (`write_file` / `patch` not added).
- Work `261010-writer-skill-test-46fdf8` STATUS is unchanged (this test does not touch the existing Work).

## Review Evidence

- Pull Request: NOT_APPLICABLE
- Review Base Commit: UNKNOWN before IMPLEMENTER Handoff (recorded as `STATUS.based_on_work_commit` of the IMPLEMENTER Handoff commit)
- Reviewed Commit: UNKNOWN before IMPLEMENTER Handoff (the IMPLEMENTER commit on `impl/261010-implementer-e2e-7e3a91`)
- Review Result: UNKNOWN before review (REVIEWER is intentionally out of scope of this Task)
- Review Reference: NOT_APPLICABLE for this Task — REVIEWER is not dispatched as part of this E2E test

### Implementation Result (IMPLEMENTER Handoff)

- Source Design Commit: `c23027f6e736515190dcc076d1b97a89abc29b0c` (Design Item `7e3a91-0001`)
- Implementation Commit: `7751b55fef95a0679e1d1ba3ce0c2fe09efe608a` on branch `impl/261010-implementer-e2e-7e3a91`
- File: `project-261010-implementer-e2e-7e3a91/implementer-e2e.txt`
- Size: 28 bytes (27 ASCII chars + single LF terminator)
- sha256: `651ef79e9e819f1d8da160cc27938fc2ca6efc1c297861338f800e13769ce149`
- Byte-equal comparison to expected `implementer delegation test\n`: pass (`diff -q` clean)
- LF only, no CRLF, no UTF-8 BOM, no trailing whitespace
- Verification method: `git cat-file blob origin/impl/...:project-.../implementer-e2e.txt | sha256sum` matches the sha256 above

## Open Issues

- none

## Notes

This Task is a Hermes native delegation E2E verification, not a product Work. The IMPLEMENTER Handoff record itself is the verification target. The Task is intentionally minimal: a single artifact file, a single impl commit, a single work Handoff commit, a single Watcher dispatch. REVIEWER is not run as part of this Task. HUMAN-only transitions (`work_state=CLOSED`, `closure_result=COMPLETE/INCOMPLETE`) are out of scope.
