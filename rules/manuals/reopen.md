# Reopen Manual

## 적용 조건

사용자가 과거에 종료(CLOSED)로 승인한 Work를 실제 사용한 뒤 결함·누락·추가 요구가 발견되어 다시 작업해야 할 때 적용한다.

## MUST — ID 유지

새 문제가 기존 Work 목적의 수정·보완·검증에 해당하면 새 Work ID를 만들지 않고 기존 Work Root ID를 유지한다.

## MUST — 과거 기록 보존

기존 종료 시점, 당시 완성/미완성 결과, Final Checklist, main 반영 Commit을 삭제하거나 과거에 종료되지 않았던 것처럼 수정하지 않고 WORK-ROOT의 종료/재개 역사에 유지한다.

## MUST — 재개 기록

재개 이유, 발견 시점, 발견 근거, 영향 범위, 새 Task 또는 재검토할 Task를 기록하고 STATUS의 `closure_result`는 현재 Cycle이 다시 열린 것을 나타내도록 null로 바꾼다.

실제 다음 행동이 설계·구현·수정이면 Work State를 PROGRESS로, 전체 Review가 먼저 필요하면 REVIEW로 매핑한다.

## CHECK — 새 Work 여부

발견된 요구가 기존 목적 보완이 아니라 독립 목적·제품·책임을 가지면 기존 Work를 재개하지 않고 새 Work Root 후보로 처리한다.
