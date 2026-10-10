# Repository Entry Manual

## 목적

새 Agent가 과거 대화나 개인 기억 없이 저장소에 진입해도 현재 작업의 기준점과 다음 행동을 같은 순서로 찾도록 한다.

## 적용 조건

저장소에서 의미 있는 작업을 새로 시작하거나, 긴 중단 뒤 다시 진입하거나, 다른 Agent에게서 Handoff를 받아 작업을 이어갈 때 적용한다.

## MUST — 진입 절차

1. 현재 Branch와 Head Commit을 확인하고 `main`, `work/<WORK-ID>`, `design/<WORK-ID>`, `impl/<WORK-ID>`, `integrate/<WORK-ID>` 중 어느 표준 작업면인지 먼저 식별한다.
2. 표준 작업면이 아닌 Branch이면 연결된 PR·Commit 목적을 확인하여 특정 Work와 무관한 Repository Maintenance 작업인지 Backup/기타 임시 Branch인지 식별하고, 목적을 하나로 확정할 수 없으면 쓰기 작업을 시작하지 않는다.
3. `integrate/<WORK-ID>`이면 Work가 HUMAN 승인으로 CLOSED인지 확인하고 `integration.md`를 우선 읽으며, Maintenance Branch이면 `rule-maintenance.md`와 연결된 PR 범위를 우선 확인한다.
4. `rules/core/OPERATING-PRINCIPLES.md`와 현재 행동에 필요한 `rules/contracts/` 정의를 확인한다.
5. `rules/indexes/MANUAL-INDEX.md`에서 자신의 역할과 현재 상황에 필요한 Manual을 선택한다.
6. Work가 존재하면 `STATUS.yaml`과 `TASK-INDEX.yaml`을 먼저 확인하여 Work State, Current Task, Last Actor, Next Actor, Open Issue, Task Priority를 식별한다.
7. 자신이 `next_actor`이면 연결된 Task 또는 Issue의 최신 Summary와 마지막 Message를 먼저 읽고 그 판단에 필요한 Design·Implementation Commit만 추가로 확인한다.
8. 자신이 `next_actor`가 아니더라도 우선순위에 있는 다른 미완료 Task를 독립적으로 수행할 수 있는지 확인할 수 있으나 동일 Task를 다른 Actor와 중복 수행해서는 안 된다.

## CHECK — 현재 할 일 없음

STATUS와 TASK-INDEX에 수행 가능한 미완료 Task가 없고 Open Issue도 자신을 기다리지 않는 경우 Work가 Final Review 후보인지 먼저 확인하고 그것도 아니면 사용자에게 다음 Work 또는 Task가 필요한지 요청한다.

## 금지

- 저장소 상태를 확인하기 전에 과거 Chat 기억만으로 작업을 재개하지 않는다.
- 현재 Branch의 책임과 목적이 불명확한 상태에서 쓰기 작업을 시작하지 않는다.
- 기존 Task가 현재 목적을 포함하는데 새 Task를 관성적으로 만들지 않는다.
- `integrate/<WORK-ID>`를 일반 구현 Branch처럼 사용하거나 Maintenance PR을 Work 종료 승인 우회 경로로 사용하지 않는다.

## 완료 조건

현재 Branch 책임, 현재 역할 또는 Integration/Maintenance 책임, 현재 Work ID, 수행할 Task 또는 Issue, 읽어야 할 추가 Manual, 기준 Head Commit이 모두 식별되면 Repository Entry가 완료된다.
