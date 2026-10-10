# Integration Manual

## 목적

사용자 종료 승인 후 Work Branch의 문제 해결 과정을 main에 통째로 넣지 않고, 당시 최신 main 위에 현재 사용에 필요한 최종 지식과 검증된 산출물만 조립하여 Final Integration PR로 전달한다.

## 진입 조건

사용자가 Work를 `종료(CLOSED)`로 승인하고 결과를 `완성(COMPLETE)` 또는 `미완성(INCOMPLETE)`으로 확정했을 때 진입한다. PR Merge는 이 사용자 결정을 대신하지 않으며 이 절차를 수행하기 위해 별도의 전용 Role을 만들 필요는 없다.

## MUST — 최신 main에서 Integration Branch 생성

종료 승인 후 원격 main의 현재 Head를 다시 확인하고 그 Commit에서 `integrate/<WORK-ID>`를 생성한다. Work 시작 시점의 오래된 main이나 design/impl Branch 자체를 Final Integration PR의 기준 Branch로 사용하지 않는다.

## MUST — main 반영 대상

현재 유효한 Rule 변경, 승인된 Design, 검증된 Project 결과, 필요한 Final Verification Summary만 Integration Branch에 선별 적용하고, 각 산출물의 source Design/Implementation Commit을 추적할 수 있게 남긴다.

## MUST — main 제외 대상

Task Thread 전체, Issue 대화 전문, 시행착오, 중간 실패, 임시 STATUS, Task Priority, Agent Handoff 로그는 Final Integration Branch와 main에 포함하지 않는다.

## MUST — Final Integration PR

Integration Branch에서 main 대상 PR을 생성하고 Work ID, 사용자 closure result, source Design/Implementation Commit, Verification 결과, 알려진 제한과 관련 Review Surface PR을 PR 본문 또는 연결된 Final Summary에서 확인할 수 있게 한다.

## CHECK — main 전진과 충돌

Integration Branch 생성 이후 main이 다시 전진했으면 Merge 전에 최신 main과의 충돌과 의미 변화를 확인한다. 기존 결과의 Behavior·Interface·State·검증에 영향이 있으면 필요한 테스트 또는 Review를 다시 수행하고, 영향이 없으면 그 근거를 기록한다.

## MUST — Merge 직전 Work Gate 재확인

Merge 직전에 Work가 여전히 `종료(CLOSED)`이고 closure result가 Final Integration PR 생성 시점과 동일하며 source Design/Implementation Commit도 변경되지 않았는지 확인한다. Work가 Reopen되었거나 새 Task·새 Design·새 Implementation 결과가 생겼으면 기존 Final Integration PR을 병합하지 않고 현재 Cycle의 Final Review와 사용자 종료 판단을 다시 완료한다.

## CHECK — Repository Gate

Branch protection, Required Review, Required Check가 실제로 활성화되어 있으면 모두 충족한 뒤 Merge한다. 해당 설정이 검증되지 않았거나 비활성화되어 있어도 사용자 종료 Gate와 이 Manual의 검증 절차를 생략해서는 안 된다.

## CHECK — INCOMPLETE 종료

사용자가 미완성으로 종료한 경우 main에 반영하는 결과가 미완료 부분을 완성된 것으로 오해하게 만들지 않는지 확인하고 필요한 제한 또는 미완료 표시를 Final Summary에 남긴다.

## MUST — Merge 이후 기록

Final Integration PR이 main에 반영되면 main Commit과 PR 참조를 Work Root의 Closure History에 추가하고, Review Surface PR이 더 이상 필요하지 않으면 병합하지 않은 상태로 닫아 Review 이력만 보존할 수 있다. 이 기록 추가는 이미 승인된 Work를 자동 Reopen하는 행동이 아니다.

## MUST — Work Branch 보존

main 반영 후에도 `work/<WORK-ID>`를 자동 삭제하지 않고 문제 발생 시 과거 판단을 추적하거나 같은 Work를 재개할 수 있도록 보존한다.

## 완료 조건

main만 읽어도 현재 사용 가능한 결과와 제한을 이해할 수 있고 Final Integration PR에서 최종 Diff와 검증을 확인할 수 있으며 과정이 필요할 때 Work Branch에서 원인을 추적할 수 있으면 통합이 완료된다.
