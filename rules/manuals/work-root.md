# Work Root Manual

## 정의

Work Root는 하나의 최초 아이디어가 설계·Task·구현·검증·종료와 재개를 거치는 전체 계보이며 `YYMMDD-<topic>-<uuid>` ID를 생성한 뒤 같은 목적 안에서는 계속 유지한다.

## MUST — 새 Work Root를 만드는 경우

현재 요청이 기존 Work의 목적을 구체화·수정·검증하는 범위를 넘어 독립된 목적·제품·책임과 자체 완료 기준을 가져야 할 때만 새로운 Work Root를 생성한다.

## CHECK — 기존 Work 유지

새 요구가 기존 Work에서 발견된 문제, 추가 설계, 구현 보완, 검증 실패, 사용 중 발견된 결함이라면 새로운 Work ID를 만들지 않고 기존 Work를 재개하거나 새 Task를 추가한다.

## MUST — Work 생성 시 기본 산출물

새 Work를 생성하면 Work ID를 발급하고 `STATUS.yaml`, `TASK-INDEX.yaml`, Work 개요 문서, 필요한 첫 Task를 Template에서 생성하며 Design과 Project Sandbox가 필요해질 때 같은 Work ID를 사용한다.

## Work State 자동 매핑

1. 사용자 승인으로 종료되었으면 `CLOSED`를 유지한다.
2. 종료되지 않았고 Final Checklist 또는 Review가 다음 핵심 행동이면 `REVIEW`로 표시한다.
3. 내부 Agent가 수행할 수 있는 행동이 하나라도 있으면 `PROGRESS`로 표시한다.
4. 내부 행동이 없고 사용자 또는 외부 입력만 필요하면 `WAITING`으로 표시한다.

Agent 간 Issue가 열려 있어도 Designer·Implementer·Reviewer 등 내부 Actor가 다음 행동을 수행할 수 있으면 Work 전체를 `WAITING`으로 낮추지 않는다.

## MUST — 종료

모든 Task와 Review가 끝났더라도 Agent는 Work를 `CLOSED`로 확정하지 않고 Final Review 결과를 사용자에게 보고하여 `COMPLETE`, `INCOMPLETE`, `계속 진행` 중 사용자 결정을 받아야 한다. 사용자가 진행 중인 Cycle을 즉시 종료하겠다고 명시하면 남은 Task·Issue·제약을 현재 근거로 정리하여 HUMAN_DECISION 절차로 이동하고, 사용자가 `CLOSED/INCOMPLETE` 또는 가능한 경우 `CLOSED/COMPLETE`를 명시적으로 승인해야 종료된다.

## 완료 후 재개

종료 후 새 문제가 발견되면 과거 종료 기록을 보존하고 같은 Work ID에 재개 이유·시점·새 Task 또는 재검토 대상을 추가한다. 실제 다음 행동이 설계·구현·수정이면 `PROGRESS`로, 전체 Review가 먼저 필요하면 `REVIEW`로 매핑한다.
