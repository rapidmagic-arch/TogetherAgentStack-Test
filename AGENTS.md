# Repository Router

이 파일은 저장소에 진입한 모든 Agent가 현재 상황에 필요한 규칙과 작업 위치를 찾도록 안내하는 최상위 Router이며, 상세 규칙을 중복 정의하지 않는다.

## MUST — Router 상속

루트 `AGENTS.md`는 저장소 전체에 적용하며, 하위 폴더에 별도 `AGENTS.md`가 있으면 그 파일은 상위 규칙을 대체하지 않고 해당 폴더의 추가 라우팅만 정의한다. 하위 폴더에 `AGENTS.md`가 없으면 가장 가까운 상위 Router를 그대로 따른다.

## MUST — 최초 진입 순서

1. 현재 Git Branch와 Head Commit을 확인한다.
2. `rules/core/OPERATING-PRINCIPLES.md`를 읽어 강제 수준·우선순위·권한 경계를 확인한다.
3. `rules/contracts/`에서 현재 작업에 필요한 ID·역할·상태·브랜치·경로·Review 결과·메시지 타입의 Canonical 정의를 확인한다.
4. `rules/indexes/MANUAL-INDEX.md`에서 현재 역할과 상황에 필요한 Manual만 선택한다.
5. 현재 Work가 존재하면 `work/<WORK-ID>/STATUS.yaml`과 `TASK-INDEX.yaml`을 먼저 읽어 현재 Task·Last Actor·Next Actor·Open Issue·우선순위를 확인한다.
6. 자신이 `next_actor`이면 연결된 Task 또는 Issue의 최신 Summary와 마지막 메시지를 먼저 읽고 필요한 Design·Implementation Commit만 추가 확인한다.
7. 작업 결과를 다른 Actor에게 넘겨야 하면 화면에 메시지만 출력하지 않고 Work Branch의 Task/Thread 기록·STATUS·우선순위를 갱신하고 Commit/Push까지 완료한다.
8. Work Root의 `종료(CLOSED)`와 `완성/미완성(COMPLETE/INCOMPLETE)`은 사용자 승인 없이 기록하지 않는다.

## CHECK — 불명확한 경우

저장소의 Canonical 정의만으로 권한·범위·우선순위·다음 행동을 하나로 결정할 수 있는지 확인하고, 가능한 선택에 따라 결과가 달라지는데 근거가 없으면 임의 추론하지 말고 사용자 판단을 요청한다.

## 하위 Router

- 규칙을 작성·수정·검토할 때는 `rules/AGENTS.md`를 추가로 읽는다.
- Template을 사용하거나 수정할 때는 `templates/AGENTS.md`를 추가로 읽는다.
- 전체 흐름 설명이 필요하면 `docs/WORKFLOW.md`를 읽는다.
- Runtime 자동화 구현 여부가 중요하면 `docs/RUNTIME-CAPABILITIES.md`를 확인한다.
- Reference가 필요할 때만 `rules/manuals/reference-lookup.md`를 읽고 `references/`를 조회한다.
