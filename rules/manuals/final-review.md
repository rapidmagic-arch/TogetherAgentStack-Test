# Final Review Manual

## 목적

개별 Task가 모두 PASS였더라도 Work 전체 결과가 목적과 설계에 맞는지 종료 직전에 다시 확인하고 사용자에게 종료/완성, 종료/미완성, 계속 진행을 판단할 충분한 정보를 제공한다.

## 진입 조건

현재 목적에 필요한 필수 Task가 더 이상 없다고 판단하고 남은 작업이 있더라도 종료 시 미완료 항목으로 명시할 수 있는 상태에서 진입한다.

## MUST — Final Checklist

- 필수 Task가 모두 완료되었거나 미완료로 명시되어 있는지 확인한다.
- 닫히지 않은 Issue가 남았는지 확인하고 남았다면 영향과 종료 가능 여부를 명시한다.
- Thread의 최종 Decision이 필요한 Design·Task·Code에 실제 반영되었는지 확인한다.
- 현재 Design과 실제 Project 결과가 주요 Interface·State·Behavior 기준에서 일치하는지 확인한다.
- 필요한 Unit/Contract/Integration/수동 검증 결과가 존재하는지 확인한다.
- 실패·제외·보류·제약 사항을 숨기지 않고 목록화한다.
- main에 반영할 최종 Design·Project 결과·Verification Summary와 Work Branch에만 남길 과정 기록을 구분한다.

## MUST — 사용자 보고

사용자에게 현재 목적, 완료된 결과, 검증 근거, 남은 미완료·제약, 종료 선택의 의미를 제공하고 HUMAN_DECISION 절차로 이동하여 사용자가 `종료/완성(CLOSED/COMPLETE)`, `종료/미완성(CLOSED/INCOMPLETE)`, `계속 진행` 중 하나를 선택할 수 있게 한다.

## 금지

Final Checklist 통과를 사용자 종료 승인과 동일시하지 않는다.

## 완료 조건

사용자 결정이 기록되면 Final Review가 완료된다. 계속 진행이면 WORK_DISCOVERY로 돌아가 다음 Task를 다시 선택하고, 종료 승인이라면 Work는 CLOSED를 유지한 채 INTEGRATION으로 이동한다.
