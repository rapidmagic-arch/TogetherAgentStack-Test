# Thread Manual

## 정의

Task Thread는 하나의 Task가 생성되어 수행·질문·결정·검증·Review를 거치는 전체 작업 기록이고, Issue Thread는 Task 안의 특정 문제를 여러 Actor가 해결하기 위해 사용하는 하위 대화 단위이다.

## CHECK — Issue를 만들지 않는 경우

Implementer가 현재 Design과 Task 범위 안에서 오류 원인을 분석하고 Method를 바꾸어 자체 해결할 수 있으면 새 Issue를 만들지 않고 같은 Task의 PROGRESS 또는 RESULT에 핵심 시도와 검증만 기록한다.

## MUST — Issue를 만드는 경우

현재 Actor의 권한만으로 결정하면 Design·목적·범위·사용자 결과가 달라지거나 다른 Actor의 명시적 판단 없이는 Task를 계속할 수 없으면 같은 Task 아래에 Issue를 생성한다.

## MUST — Issue 최초 기록

Issue를 열 때 현재 상황, 관찰된 문제, 이미 시도한 방법과 결과, 필요한 판단 질문, 영향 범위, Task ID, 관련 Design Ref, 현재 기준 Commit을 기록하여 다음 Actor가 추가 설명 없이 판단을 시작할 수 있게 한다.

## MUST — Message 기록

각 Thread Message는 Message Type, Actor Role, 시각, Task ID, 필요 시 Issue ID와 기준 Commit을 포함하고 `QUESTION`과 `DECISION`은 질문 범위와 결정 적용 범위를 서로 대응시킨다.

## MUST — Decision 이후

Decision이 작성되면 누가 어느 Design·Task·Code에 반영할지 명확히 하고 실제 반영과 검증이 끝나기 전에는 Issue를 닫힌 것으로 취급하지 않는다.

## Issue 종료 조건

1. 최종 판단이 하나로 명확해야 한다.
2. 필요한 Design·Task·Code 변경이 실제로 반영되어야 한다.
3. 반영 위치와 Commit을 확인할 수 있어야 한다.
4. 필요한 테스트 또는 검증이 수행되어야 한다.
5. 문제를 제기한 Actor와 결과를 적용한 Actor가 최종 결과를 확인해야 한다.
6. `CLOSE.md`에 문제·결정·반영 위치·검증·확인 Actor를 요약해야 한다.

위 조건을 충족한 `CLOSE.md`가 존재하면 해당 Issue가 종료된 것으로 판단하며 별도의 Issue 상태 코드를 만들지 않는다.

## MUST — Issue 종료 후 복귀

Issue가 닫힌 뒤 같은 Task에 추가 설계·구현·수정이 필요하면 EXECUTION으로, Task 결과가 Review 가능한 상태이면 TASK_REVIEW로, 아직 HUMAN 전용 판단이 남아 있으면 HUMAN_DECISION으로 이동한다. Issue 종료 자체만으로 Task 완료나 PASS를 의미하지 않는다.

## MUST — Thread와 Design 분리

Thread의 대화 전체를 Design에 복사하지 않고 최종적으로 유효한 설계 결정과 필요한 근거만 Design에 반영한다.
