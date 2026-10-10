# Review Manual

## 목적

Reviewer가 구현 결과를 현재 Task와 Design에 대조하고 GitHub PR의 Diff·inline review·check를 필요한 검토 증거로 활용하되, 구현 수정·설계 문제·사용자 판단과 Work Canonical을 혼동하지 않도록 한다.

## MUST — Review 입력

Task 목적·Condition·Out of Scope·Design Ref·Implementation Result Commit·Verification 결과·Open Issue를 확인하고, Review Surface PR이 연결되어 있으면 PR 전체의 최신 상태가 아니라 Work가 지정한 `review_base_commit..reviewed_commit` 범위와 최종 결과 상태를 확인한다.

## MUST — PR 경계

PR은 변경분을 보는 Review Surface이며 Task의 Canonical 판정 원장이 아니다. Reviewer는 `rules/contracts/git-review.yaml`에 따라 PR 번호 또는 URL, review_base_commit, reviewed_commit, Review 결과와 근거를 Work Task/Event에 기록한다.

## CHECK — inline comment로 끝낼 수 있는 문제

현재 Design과 Task Condition을 유지하는 코드·설정·문서의 국소 문제라면 PR inline thread에서 수정과 확인을 진행할 수 있다. 반대로 판단에 따라 Design·범위·사용자 결과가 달라지거나 다른 Actor 권한이 필요하면 PR comment를 Work Issue에 연결하고 Issue/Thread 절차로 전환한다.

## MUST — 검토 범위 고정

GitHub의 Approve·Request Changes·Comment만으로 PASS를 확정하지 않는다. Reviewer는 Task Review가 승인하는 변경 시작점인 `review_base_commit`과 실제 검토한 마지막 SHA인 `reviewed_commit`을 기록하고 `review_base_commit..reviewed_commit` 전체 Diff와 최종 결과를 확인한다. 같은 Task의 REWORK에서는 원래 Task 변경 범위를 잃지 않도록 review_base_commit을 유지하며 기준점이 바뀌면 이유를 기록하고 새 범위 전체를 다시 검토한다.

## CHECK — stale Review

reviewed_commit 이후 PR Head에 새 Commit이 추가되면 해당 변경이 현재 Task Review 범위·행동·검증에 영향을 주는지 확인하여 영향이 있으면 새 reviewed_commit까지 다시 검토하고, 영향이 없으면 기존 판정을 유지하는 근거를 Work에 기록한다.

## CHECK — Reviewer identity

PR 작성자와 Reviewer가 같은 GitHub 사용자·App·Bot identity를 사용한다면 GitHub의 승인 표시 자체를 독립 검토 증거로 간주하지 않고, 현재 REVIEWER Role이 수행한 비교·검증 근거와 판정은 Work에 별도로 기록한다.

## MUST — 판정 코드

Review 결과는 `rules/contracts/review-results.yaml`의 PASS, REWORK, DESIGN_ISSUE, USER_DECISION_REQUIRED 중 하나만 사용하고 각 코드의 의미를 이 Manual에서 새로 정의하지 않는다.

## MUST — 근거 기록

Review는 판정 코드만 남기지 않고 어떤 Condition·Design·Test·PR Diff 근거로 판정했는지 기록하고 REWORK나 DESIGN_ISSUE이면 다음 Actor가 바로 행동할 수 있는 구체 대상과 기대 수정 결과를 적는다.

## MUST — 다음 행동

- PASS이면 Task SUMMARY에 Review 범위와 PR 근거를 포함해 최신화하고 TASK-INDEX의 `completed_at`을 기록한 뒤 PRIORITY_REFRESH로 이동한다.
- REWORK이면 같은 Task와 review_base_commit을 유지하고 `next_actor=IMPLEMENTER`로 넘겨 EXECUTION으로 복귀한다.
- DESIGN_ISSUE이면 같은 Task에 Issue를 생성하거나 기존 Issue를 재개하고 `next_actor=DESIGNER`로 넘겨 ISSUE_HANDOFF 절차를 따른다.
- USER_DECISION_REQUIRED이면 질문 범위, 선택 영향, 판단 적용 대상과 사용자 응답 후 재개할 Task/Issue를 Work에 기록하고 `next_actor=HUMAN`으로 넘겨 HUMAN_DECISION 절차를 따른다.

## 금지

Reviewer는 구현이 마음에 들지 않는다는 이유만으로 독립 새 기능을 Review 요구사항에 추가하지 않으며, PR thread를 Resolve했다는 이유만으로 Task PASS 또는 Work Issue 종료를 확정하지 않는다.
