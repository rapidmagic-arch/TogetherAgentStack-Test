# Implementation Manual

## 목적

Implementer가 현재 Task와 채택된 Design을 실제 제품 구조에 구현하고 GitHub PR을 사용할 수 있을 때 변경 Diff를 Review에 활용하되 세부 문제는 자율적으로 해결하고 설계·권한 경계를 넘는 문제는 공용 Thread로 전달하도록 한다.

## MUST — 시작 입력

구현 전 현재 Task의 목적·In Scope·Out of Scope·Condition·Design Ref·기준 Commit·Verification 기준을 확인하고 직접 관련된 이전 Task Summary만 추가로 읽는다.

## MUST — Sandbox 구조

실제 파일은 `project-<WORK-ID>/` 안에서 제품의 Module·Component·Test·Config 책임에 맞춰 배치하고 Task 번호를 제품 디렉터리 구조로 사용하지 않는다.

## MAY — 자율 변경 범위

현재 Task 목적과 Design을 유지하는 범위에서 Method 변경, 오류 수정, 세부 리팩터링, 테스트 추가, 진단 로깅, 파일 구조의 자연스러운 정리는 Implementer가 자체 판단할 수 있다.

## CHECK — 새 Task 후보

구현 중 새 Module·독립 Component·상위 구조·별도 기능 책임이 필요해 현재 Task와 독립 검증할 수 있다면 현재 Task에 몰래 포함하지 않고 Task Manual에 따라 새 Task 후보로 처리한다.

## CHECK — Review Surface PR

GitHub PR 기능을 사용할 수 있고 구현 변경이 Diff 검토에 의미가 있으면 `impl/<WORK-ID>`의 기존 Review Surface PR을 재사용하거나 Draft PR을 생성하고, PR이 최종 main 병합용이 아니라 검토용임을 본문에 명시한다. PR을 만들 수 없더라도 Commit Diff를 기준으로 Review할 수 있으므로 Task 진행을 임의 중단하지 않는다.

## MUST — 막힌 경우

다른 Actor의 판단 없이는 계속할 수 없으면 화면이나 PR comment에 질문만 남기지 않고 Issue Thread에 현재 상황·문제·시도·필요 판단·영향 범위·현재 Commit과 관련 PR thread를 기록하고 STATUS의 `next_actor`를 적절한 Actor로 갱신하여 공용 Work Branch에 Push한다.

## CHECK — 병렬 진행

한 Issue 때문에 현재 Task 일부가 막혀도 다른 Task 또는 같은 Task의 독립 영역을 안전하게 계속할 수 있는지 확인하고 가능하면 Work 전체를 불필요하게 WAITING으로 만들지 않는다.

## MUST — Result 제출

Review 요청 전 현재 Task에서 Reviewer가 승인해야 할 전체 변경이 시작되기 직전 Commit을 `review_base_commit`으로 고정하고, 구현 Result의 마지막 Commit을 `reviewed_commit`으로 기록한다. 구현 변경 요약, Verification 실행 결과, 남은 제한, 관련 Issue, Design Ref, 사용한 PR 번호 또는 URL과 함께 두 SHA를 Task RESULT에 기록하고 STATUS의 `next_actor`를 REVIEWER로 갱신한다. 같은 Task가 REWORK로 돌아오면 review_base_commit은 유지하고 reviewed_commit만 새 결과 Commit으로 전진시킨다.
