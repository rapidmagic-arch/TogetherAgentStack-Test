# Branch Collaboration Manual

## 목적

공용 Task/Thread와 설계·구현 산출물이 서로 다른 브랜치에 존재하더라도 Agent가 어느 브랜치의 어떤 Commit을 읽고 다음 작업을 해야 하는지 추론하지 않도록 연결 방식을 고정한다.

## Branch 책임

- `main`: 사용자 승인 후 현재 유효한 규칙·Design·Project 결과를 보존한다.
- `work/<WORK-ID>`: STATUS, TASK-INDEX, Task, Issue Thread, Handoff 기록의 Canonical이다.
- `design/<WORK-ID>`: `design-<WORK-ID>/` 아래 설계 산출물의 작업 브랜치이다.
- `impl/<WORK-ID>`: `project-<WORK-ID>/` 아래 실제 구현·테스트 산출물의 작업 브랜치이다.

## MUST — Work 시작 기준점

새 Work의 work/design/impl 브랜치는 같은 승인된 main 기준 Commit에서 시작하고, Work 기록에는 그 기준 Commit을 남겨 세 브랜치가 어느 기준에서 갈라졌는지 추적할 수 있게 한다.

## MUST — Design에서 Implementation으로 전달

Designer가 설계를 변경하면 Design Branch에 Commit하고, 공용 Work Branch의 관련 Task 또는 Issue에 `design_commit`과 적용 Design Item을 기록한 뒤 STATUS의 `active_design_commit`을 갱신한다.

Implementer는 Design Branch 전체를 추측해 최신본으로 사용하지 않고 Work Branch가 가리키는 `active_design_commit`의 Design을 기준으로 구현한다.

## MUST — Implementation에서 Review로 전달

Implementer가 결과를 제출하면 Implementation Branch에 Commit하고, Work Branch의 Task RESULT에 `implementation_commit`과 Verification 결과를 기록한 뒤 STATUS의 `active_impl_commit`을 갱신한다.

Reviewer는 임의의 최신 Implementation Branch Head가 아니라 Work Branch가 명시한 Implementation Commit을 검토 기준으로 사용한다.

## CHECK — 기준이 바뀐 경우

Implementer가 작업하는 동안 `active_design_commit`이 변경되면 새 Design이 현재 구현에 미치는 영향을 확인하고, 기존 구현을 그대로 유지할 수 있는지 근거를 기록한 뒤 계속하며, 영향이 불명확하면 Issue로 전환한다.

## MUST — Thread 원본

Design·Implementation Branch에는 공용 Thread 복사본을 운영하지 않고 모든 질문·Decision·Handoff는 `work/<WORK-ID>`에 기록한다.

## MUST — main 통합

Work Branch를 main에 통째로 병합하지 않고 사용자 승인 후 Design Branch와 Implementation Branch의 최종 산출물 중 현재 유효한 파일만 Integration Manual에 따라 main에 선별 반영한다.
