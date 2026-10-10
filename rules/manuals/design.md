# Design Manual

## 목적

Designer가 현재 Work의 목적을 구현 가능한 결정으로 구체화하고 구현 중 발생한 설계 Issue에 현재 기준을 명확하게 제공하며, 설계 문서 Diff 검토가 유용한 경우 GitHub PR을 보조 Review Surface로 사용할 수 있게 한다.

## MUST — Designer 진입 순서

STATUS의 `next_actor`가 DESIGNER이면 전체 Design 문서를 처음부터 다시 읽기 전에 STATUS가 연결한 Open Issue와 Implementer의 마지막 Message를 먼저 읽고 그 판단에 직접 필요한 Task·Design Item·Implementation Commit만 추가 확인한다.

## MUST — Design Item 작성

일반 설계는 `templates/design-default/`를 시작점으로 사용하고 목적, 범위, 문제, 요구 결과, 제약, 설계 결정, Interface/Data/State, Verification Criteria, 미확정 사항을 최소 항목으로 유지한다.

## CHECK — 특수 구조 사용

기본 Template이 표현하려는 설계의 의미를 왜곡하거나 핵심 구조를 표현하기 어렵다면 다른 문서 구조를 사용할 수 있으나 목적·범위·결정·검증 기준·미확정 사항을 제거하지 않고 특수 구조를 사용한 이유를 기록한다.

## CHECK — Design Review Surface PR

GitHub PR 기능을 사용할 수 있고 설계 변경의 Diff 검토가 실제 판단에 도움이 되면 `design/<WORK-ID>`의 Draft Review Surface PR을 생성하거나 재사용할 수 있다. PR comment는 설계 검토 근거로 사용할 수 있지만 채택된 Decision의 Canonical은 Work Issue/Task와 Design Item이며 PR thread만으로 설계 결정을 확정하지 않는다.

## MUST — Issue 답변

설계 Issue에 답할 때 단순 조언을 남기지 않고 최종 Decision, 선택 근거, 적용 범위, 변경되는 Design Item, 구현자가 다시 시작할 기준 Commit과 관련 Review Surface PR이 있으면 그 참조를 Thread에 연결한다.

## CHECK — 사용자 권한

설계 선택이 기존 Work 목적을 넘어 제품 범위·상위 책임·사용자 권한을 변경하면 Designer가 직접 확정하지 않고 선택지, 각 선택의 영향, 판단이 적용될 Task/Issue와 응답 후 복귀 지점을 Work에 기록하여 HUMAN_DECISION 절차로 넘긴다.

## MUST — Handoff

설계 결정이 구현 가능해지면 Design 변경을 Commit하고 Issue에 Design Commit을 기록하며 STATUS의 `next_actor`를 IMPLEMENTER로 갱신한 뒤 공용 Work Branch 기록까지 Push한다.

## 완료 조건

다음 Actor가 Issue와 Design Commit만 읽어도 무엇을 구현해야 하는지, 무엇이 바뀌지 않았는지, 어떤 조건으로 검증할지 알 수 있고 필요한 경우 설계 PR Diff 위치까지 찾을 수 있으면 Designer 행동이 완료된다.
