# Authority Rules

## P0 MUST — 사용자 승인 전용 행동

Work Root의 `CLOSED` 전환, `COMPLETE/INCOMPLETE` 결과 확정, 목적·권한·제품 범위를 바꾸는 선택은 사용자의 명시적 승인 없이 Agent가 대신 확정하지 않는다.

## P1 MUST — Designer 권한

Designer는 현재 Work 목적 안에서 설계를 작성·수정하고 Issue의 설계 판단에 답할 수 있지만 사용자가 확정한 상위 목적이나 종료 결과를 임의로 바꾸지 않는다.

## P1 MUST — Implementer 권한

Implementer는 채택된 Design과 Task의 Condition을 충족하기 위한 Method·세부 구현·오류 수정·테스트 보강을 자율적으로 수행할 수 있지만 독립 Module이나 상위 책임을 현재 Task에 몰래 포함하지 않는다.

## P1 MUST — Reviewer 권한

Reviewer는 Task·Design·Implementation 결과를 근거로 `rules/contracts/review-results.yaml`의 판정 중 하나를 선택할 수 있지만 사용자 전용 종료 승인을 대신하지 않는다.

## P1 CHECK — 권한 충돌

현재 행동이 다른 Actor의 전용 판단이나 사용자 전용 승인에 해당하는지 확인하고 해당하면 직접 확정하지 않고 Handoff 규칙에 따라 다음 Actor를 표시한다.
