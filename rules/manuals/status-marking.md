# Status and Priority Marking Manual

## 목적

Designer·Implementer·Reviewer가 작업을 끝내거나 넘길 때 현재 상태와 다음 행동을 동일한 표식으로 남겨 다음 Agent가 Thread 전체를 읽기 전에 현재 상황을 즉시 파악하도록 한다.

## 정의

`STATUS.yaml`은 현재 Work를 빠르게 찾기 위한 Projection이고, `TASK-INDEX.yaml`은 현재 Task 목록·완료 여부·실행 우선순위를 빠르게 찾기 위한 Projection이며 두 파일은 Task·Thread·Review·Git 이력을 대체하지 않는다.

## MUST — 갱신 Trigger

다음 사건이 발생할 때마다 Agent는 STATUS와 TASK-INDEX가 실제 원본 기록과 일치하는지 다시 확인하고 필요한 값과 확인 시각을 갱신한다.

1. Task 작업을 한 의미 있는 단위 수행한 뒤 작업을 중단하거나 다른 행동으로 전환할 때.
2. Issue를 생성·답변·반영·검증·종료할 때.
3. `next_actor`가 바뀌는 Handoff가 발생할 때.
4. Review 결과가 기록될 때.
5. 새 Task가 생성되거나 기존 Task가 완료될 때.
6. Work가 Final Review 또는 HUMAN 판단 단계로 이동할 때.
7. Work가 CLOSED되어 Integration 대상으로 이동할 때.
8. 종료된 Work가 재개될 때.

## MUST — STATUS 필드 의미

- `current_task`: 현재 Handoff 또는 실행의 직접 대상 Task이며 대상이 없으면 null을 사용한다.
- `last_actor`: STATUS를 갱신하기 직전 마지막 의미 있는 행동을 기록한 Role이다.
- `next_actor`: 다음 저장소 진입 시 우선 행동해야 하는 Role이며 HUMAN의 추가 응답이 실제로 필요한 동안에만 HUMAN을 기록한다.
- `condition`: 지금 왜 이 Work 상태와 다음 행동이 필요한지 한 문장으로 설명하며 HUMAN 판단을 기다릴 때는 판단 질문과 응답 후 재개할 Task 또는 Issue를 식별할 수 있게 쓴다.
- `open_issue`: 현재 Handoff의 직접 원인이 되는 닫히지 않은 Issue가 없으면 null을 사용한다.
- `based_on_work_commit`: 이번 Projection을 계산하기 전에 Agent가 읽은 Work Branch Head이며 STATUS를 포함하는 새 Commit 자신의 SHA를 미리 기록하려고 사용하지 않는다.
- `active_design_commit`: 현재 Task가 기준으로 삼는 Design Commit이 있으면 기록한다.
- `active_impl_commit`: 현재 Review 또는 Handoff가 참조하는 Implementation Commit이 있으면 기록한다.
- `priority_head`: TASK-INDEX의 현재 우선순위에서 가장 앞선 미완료 Task이며 실행 가능한 Task가 없으면 null을 사용한다.
- `closure_result`: 현재 Cycle이 종료된 경우에만 COMPLETE 또는 INCOMPLETE를 기록하고 재개하면 null로 되돌리며 과거 종료 결과는 WORK-ROOT의 역사에서 보존한다.

## MUST — HUMAN 판단 대기 매핑

HUMAN의 추가 응답이 필요한 경우에만 `next_actor=HUMAN`을 유지한다. 다른 내부 Actor가 안전하게 수행할 수 있는 독립 행동이 남아 있으면 Work는 PROGRESS를 유지하고, 내부 행동이 전혀 없고 HUMAN 응답만 있어야 진행할 수 있으면 WAITING으로 매핑한다. HUMAN 답변이 이미 기록되었거나 최초 사용자 요청 자체가 충분한 결정을 포함하면 답변을 적용할 Task·Issue·Priority·Review 지점을 확인하고 next_actor와 Work State를 실제 다음 행동에 맞게 즉시 다시 계산한다.

## MUST — 우선순위 재평가

각 Agent 행동 경계에서 남은 미완료 Task를 다시 살펴보고 순서가 명확하면 `priority_order`를 최신화하며 순서가 바뀌지 않았더라도 마지막 검토 시각을 기록한다.

## CHECK — 사용자 판단

우선순위 선택에 따라 범위·결과·비용이 실질적으로 달라지고 Canonical 근거가 없어 하나로 정할 수 없으면 Priority를 임의 변경하지 않고 사용자 판단 요청을 `condition`에 기록하고 추가 응답이 필요하면 `next_actor=HUMAN`으로 표시한다.

## 완료 조건

STATUS와 TASK-INDEX만 읽은 새 Agent가 현재 Work 상태, 다음 Actor, 가장 먼저 볼 Task/Issue, 기준 Design/Implementation Commit을 정확히 찾을 수 있으면 Marking이 완료된다.
