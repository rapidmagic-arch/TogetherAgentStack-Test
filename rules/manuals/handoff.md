# Handoff Manual

## 정의

Handoff는 한 Actor가 자신의 역할 범위에서 수행 가능한 행동을 끝내고 다른 Actor가 저장소만 읽어 다음 행동을 이어가도록 작업 책임을 넘기는 과정이다.

## MUST — Handoff에 필요한 기록

1. 현재 Task 또는 Issue에 마지막 행동과 결과를 기록한다.
2. 다음 Actor가 판단하는 데 필요한 Design Ref, Result Commit, Test Result, Open Question과 Review Surface PR이 있으면 그 PR 참조를 연결한다.
3. STATUS의 `last_actor`, `next_actor`, `condition`, `open_issue`, `last_event`, `based_on_work_commit`을 실제 기록과 맞춘다.
4. Task Priority가 변했으면 TASK-INDEX와 현재 최우선 순서의 이유를 최신화한다.
5. Push 직전에 원격 Work Branch Head가 자신이 읽은 기준과 달라졌는지 확인하고, 달라졌으면 강제 덮어쓰지 말고 최신 기록을 다시 읽어 충돌을 해소한다.
6. 모든 변경을 Commit하고 원격 Work Branch에 Push한다.

## MUST — PR은 Handoff 원장이 아니다

PR notification, Review request, inline comment만 남기고 Work 기록을 생략하지 않는다. 다음 Actor에게 판단 책임을 넘겨야 하는 PR comment는 관련 Task 또는 Issue에 PR 위치와 필요한 판단을 연결하여 Repository Entry만으로 발견할 수 있게 한다.

## MUST — 구현자 중단 Handoff

Implementer가 막힌 경우 질문 문장만 남기지 않고 문제·시도·필요 판단·영향 범위·Commit까지 Issue에 기록해야 Designer 또는 Reviewer가 추가 설명 없이 판단할 수 있다.

## MUST — Designer 응답 Handoff

Designer가 Decision을 내린 경우 Thread 답변만 남기지 않고 필요한 Design 반영·Design Commit·적용 범위·next_actor 갱신까지 완료한다.

## CHECK — 사용자 Handoff

결정이 HUMAN 전용인지 확인하고 해당하면 선택지·각 선택의 영향·현재 안전한 기본 상태를 한 번에 이해할 수 있게 기록한다.

## 완료 조건

다음 Actor가 별도 Chat 또는 GitHub notification 없이 Repository Entry 절차만 수행하여 자신이 해야 할 행동, 기준 Commit과 필요한 PR Review 위치를 찾을 수 있으면 Handoff가 완료된다.
