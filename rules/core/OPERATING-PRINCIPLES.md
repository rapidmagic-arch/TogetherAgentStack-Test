# Operating Principles

이 문서는 모든 Agent가 항상 적용해야 하는 최소 운영 원칙을 정의하며, 용어의 특별한 의미는 `rules/contracts/TERMS.md`, 우선순위의 Canonical은 `rules/contracts/priorities.yaml`을 따른다.

## 강제 수준

- `MUST`: 조건이 성립하면 반드시 수행하며, 누락되면 해당 행동·전이·완료를 유효한 것으로 인정하지 않는다.
- `CHECK`: 현재 상황이 조건에 해당하는지 반드시 확인하고, 해당하면 연결된 행동을 반드시 수행한다.
- `MAY`: 상위 규칙과 충돌하지 않고 현재 목적에 도움이 되는 경우 선택할 수 있다.

## 우선순위

`P0 > P1 > P2 > P3` 순으로 적용하며, 낮은 우선순위 규칙은 높은 우선순위 규칙을 변경하거나 우회할 수 없다.

## P0 MUST — 사용자 권한

Work Root의 최종 종료 여부와 `COMPLETE/INCOMPLETE` 결과는 Task·테스트·Review가 모두 끝났더라도 사용자의 명시적 승인으로만 확정한다.

## P0 MUST — Canonical 단일화

ID·Role·Work State·Review Result·Branch·Path·Message Type·특수 용어처럼 여러 문서가 공통으로 사용하는 값은 `rules/contracts/`의 한 위치에서만 Canonical로 정의하고 다른 문서는 그 값을 재정의하지 않는다.

## P0 MUST — main의 의미

`main`은 현재 사용자가 신뢰하고 사용할 수 있는 규칙·승인된 설계·검증된 결과를 보존하며, Task Thread·질문·시행착오·중간 실패처럼 문제 해결 과정 자체를 최종 지식으로 간주하지 않는다.

## P1 MUST — 공용 Work 기록

Task·Issue Thread·현재 상태·우선순위·Agent Handoff는 `work/<WORK-ID>`를 Canonical로 사용하며 Design 또는 Implementation 브랜치에 별도의 Thread 원본을 만들지 않는다.

## P1 MUST — 행동 완료 계약

Agent의 행동은 실제 산출물 저장, 관련 Task/Thread 기록, STATUS 및 필요한 우선순위 갱신, Commit/Push까지 끝나 다음 Actor가 저장소만 보고 이어서 작업할 수 있을 때 완료된다.

## P1 MUST — 임의 추론 금지

현재 저장소의 Canonical 정보만으로 범위·권한·우선순위·다음 행동을 하나로 결정할 수 없고 선택에 따라 결과가 달라지는 경우 Agent는 관례나 기억으로 값을 채우지 않고 사용자에게 판단을 요청한다.

## P2 MUST — 과정과 결과 분리

Thread에는 문제 해결 과정을 남기고 Design·Project·Final Summary에는 현재 유효한 결정과 검증 결과만 반영하여 과정 기록과 현재 진실을 서로 대체하지 않게 한다.

## P3 CHECK — Reference 조회

현재 Repository Rule·Design·Task만으로 안전하게 작업할 수 있는지 먼저 확인하고 추가 방법론이 실제로 필요할 때만 `references/`를 조회하며 Reference를 읽었다는 사실만으로 현재 프로젝트 규칙이나 설계로 채택해서는 안 된다.
