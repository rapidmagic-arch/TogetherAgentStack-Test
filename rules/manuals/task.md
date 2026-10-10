# Task Manual

## 정의

Task는 현재 Work에서 실제로 수행하고 검증할 수 있는 기본 작업 단위이며, 미래 작업 전체를 처음부터 고정하는 계획표가 아니라 이전 결과에 따라 순차적으로 성장하는 작업 원장이다.

## Commit 용어

- `Base Commit`: Task를 생성하거나 실행 기준을 잡을 때의 입력 기준 Commit이며, Task가 어떤 Repository 상태에서 시작했는지 추적하기 위한 값이다.
- `Review Base Commit`: Reviewer가 PASS 여부를 판단할 전체 변경 범위가 시작되기 직전 Commit이며, `review_base_commit..reviewed_commit`의 시작점이다. Task의 Base Commit과 같을 수 있지만 Design 반영·선행 Commit·다른 역할 작업 때문에 다를 수 있으므로 자동으로 같은 값으로 간주하지 않는다.
- `Reviewed Commit`: Reviewer가 실제 판정한 변경 범위의 마지막 Commit이며 Review 이후 새 Commit이 생기면 해당 Commit까지 자동 승인된 것으로 간주하지 않는다.

## MUST — Task 생성 전 확인

새 Task를 만들기 전에 기존 Task의 목적·Condition·현재 Result를 확인하여 새 요구가 기존 Task를 끝내기 위한 세부 변경인지 독립된 결과물인지 판정한다.

## 기존 Task 안에서 계속하는 기준

Condition의 세부 보완, Method 변경, 오류 수정, 리팩터링, 테스트 추가, 검증 실패 수정, 같은 Module 안의 세부 구현처럼 현재 Task의 동일 목적을 완성하기 위한 변화는 새 Task를 만들지 않고 같은 Task에서 처리한다.

## 새 Task를 만드는 기준

새 Module·독립 Component·별도 기능 책임·상위 구조·독립적으로 완료 여부를 판단할 수 있는 결과처럼 현재 Task와 분리된 목적과 검증 기준이 생기면 새로운 Task를 생성한다.

## CHECK — 경계가 애매한 경우

같은 Task로 포함하면 원래 목적과 완료 조건이 설명하기 어려워지고, 새 Task로 분리하면 독립 검증 기준을 만들 수 있는지 확인한 뒤에도 하나로 정해지지 않으면 사용자에게 범위 결정을 요청한다.

## MUST — 새 Task 입력

Task에는 최소한 ID, 목적, In Scope, Out of Scope, Condition, 관련 Design Ref, Base Commit, 기대 Result, Verification 기준을 기록한다.

## MUST — 이전 Task 확인

새 Task를 시작할 때 TASK-INDEX의 이전 Task Summary를 확인하고 현재 Task와 직접 관련된 이전 Task만 전문·Issue Close·Design Ref까지 확장해서 읽는다.

## MUST — 우선순위 갱신

의미 있는 작업 또는 Review가 끝날 때마다 남은 미완료 Task를 다시 확인하고 현재 실행 순서가 명확하면 TASK-INDEX를 최신화하며 현재 최우선 Task의 이유를 완성형 문장으로 기록한다.

## CHECK — 우선순위 사용자 판단

두 개 이상의 Task 중 어느 것을 먼저 수행하는지에 따라 설계·범위·비용·사용자 결과가 달라지는데 Repository 근거만으로 순서를 정할 수 없으면 임의로 고르지 않고 HUMAN_DECISION 절차로 사용자에게 우선순위를 요청한다.

## Task 완료 조건

Result와 Verification 근거가 기록되고 Reviewer가 `review_base_commit..reviewed_commit` 범위를 기준으로 PASS를 판정하며 SUMMARY가 최신화되면 TASK-INDEX의 `completed_at`에 완료 시점을 기록한다. Task 완료는 Work 종료를 의미하지 않는다.
