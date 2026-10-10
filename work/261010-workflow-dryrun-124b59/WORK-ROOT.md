# Work Root `261010-workflow-dryrun-124b59`

이 Work는 제품 기능 개발이 아니라 `TogetherAgentStack` Template이 규정한 Lifecycle (`Work 생성 → Design → Implementation → Review → HUMAN 종료 판단 → Integration`)을 실제 Repository 기록과 Git Branch 흐름으로 끝까지 수행할 수 있는지 검증하는 1회차 Dry-run이다.

## 목적

`TogetherAgentStack-Test` 저장소에서 `work/<WORK-ID>`, `design/<WORK-ID>`, `impl/<WORK-ID>` Branch와 `work/<WORK-ID>/STATUS.yaml`, `TASK-INDEX.yaml`, `tasks/<TASK-ID>/TASK.md` 등 최소 Work Root 산출물을 생성하고, 단일 Task (`124b59-T0001`)를 Design → Implementation → Review → Priority Refresh → Final Review까지 진행한 뒤 사용자 종료 판단을 받아 Lifecycle을 종료한다.

## 검증 범위

이번 회차에서 검증하는 항목은 아래와 같다.

- Work ID, Task ID 발급이 `rules/contracts/identifiers.yaml` 형식과 불변성 규칙을 따르는가
- 세 Branch가 동일한 base main Commit에서 시작되는가 (`branches.yaml` `creation.work_rule`)
- `work/<WORK-ID>/STATUS.yaml`과 `TASK-INDEX.yaml`의 필드와 갱신 흐름이 Contract와 정합하는가
- `design/<WORK-ID>/` Branch에서 작성한 최소 Design Commit SHA가 Work Canonical에 기록되는가
- `impl/<WORK-ID>/` Branch에서 `project-<WORK-ID>/hello.txt`를 생성·검증하고 그 Commit SHA가 Work Canonical에 기록되는가
- Review 단계에서 `review_base_commit..reviewed_commit` 범위가 실제 Commit SHA로 고정되어 PASS/REWORK가 판정되는가
- Final Review 후 사용자 종료 승인 없이 `integrate/<WORK-ID>`가 생성되지 않는가 (P0 사용자 권한)

## 검증 범위 밖 (1회차 한정)

다음은 이번 Dry-run에서 활성화하거나 검증하지 않는다.

- Cron / Watcher / 자동 Writer / Kanban 대체 / Webhook / 별도 adapter
- Runtime 자동화 (Hermes 네이티브 Git/Workflow/PR 자동화 조사 결과는 본 Work와 무관)
- Final Integration PR의 실제 병합 (사용자 종료 승인 전에는 생성하지 않음)

## base main Commit

`16f8e619472e434468e2b305eaddb44012dce2ad` (2026-10-10, `TogetherAgentStack-Test` 초기 commit)

## 종료 조건

사용자 명시적 승인 없이 `CLOSED` / `COMPLETE` / `INCOMPLETE`을 기록하지 않는다. Final Review 결과를 사용자에게 보고한 뒤 사용자 승인 또는 추가 지시를 대기한다.