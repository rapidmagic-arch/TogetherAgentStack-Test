# Scenario Index

이 문서는 자주 발생하는 상황에서 어느 Manual로 이동해야 하는지 안내하며 상세 행동 자체는 해당 Manual을 따른다.

| 상황 | 즉시 판단 | 이동할 Manual |
|---|---|---|
| 구현자가 설계 판단 때문에 멈춤 | 같은 Task 안의 Issue 후보이며 PR comment만 남기지 않음 | `thread.md` + `handoff.md` + `status-marking.md` |
| Designer가 저장소에 진입 | `next_actor=DESIGNER`인 최신 Issue 우선 확인 | `design.md` |
| 구현 중 단순 오류 발생 | 현재 Condition/Method 범위면 같은 Task | `implementation.md` + `task.md` |
| 구현 중 새 Module 필요 | 독립 결과·책임이면 새 Task 후보 | `task.md` |
| Issue 답변이 도착 | 답변만으로 Close 금지, 실제 반영 확인 | `thread.md` |
| Issue가 닫힘 | 추가 실행 필요면 EXECUTION, 결과가 Review 가능하면 TASK_REVIEW | `thread.md` + 원래 실행 Manual |
| Design이 구현 중 변경됨 | active_design_commit 변화 영향 확인 | `branching.md` |
| 구현 Result가 Review로 넘어감 | `review_base_commit..reviewed_commit` 범위를 고정 | `branching.md` + `review.md` |
| PR inline comment가 국소 구현 문제 | Design/Condition 유지 시 PR thread에서 수정 가능 | `review.md` |
| PR comment가 설계·범위 판단 필요 | Work Issue로 연결하여 Canonical 판단 수행 | `review.md` + `thread.md` |
| Review 후 PR Head에 새 Commit 추가 | reviewed_commit 이후 영향 확인, 필요 시 재Review | `review.md` |
| Review에서 구현만 문제 | 같은 Task REWORK, review_base_commit 유지 | `review.md` |
| Review에서 설계가 문제 | DESIGN_ISSUE 생성 | `review.md` + `thread.md` |
| Review/Issue/Priority에서 사용자 전용 판단 필요 | `next_actor=HUMAN`, 질문·영향·복귀 지점 기록 | `handoff.md` + `status-marking.md` + 원래 Manual |
| HUMAN 답변 도착 | 답변 적용 대상과 복귀 지점을 확인해 EXECUTION/ISSUE/PRIORITY/Final Review로 복귀 | `status-marking.md` + 원래 Manual |
| Task가 여러 개 남아 순서가 애매 | 근거 있으면 재정렬, 결과 달라지면 HUMAN 판단 | `task.md` + `status-marking.md` |
| Agent가 작업을 끝내거나 넘김 | STATUS와 Priority를 반드시 재검토 | `status-marking.md` + `handoff.md` |
| 모든 필수 Task가 끝난 것 같음 | Final Checklist 수행 | `final-review.md` |
| 사용자가 종료 승인 | Work는 CLOSED 유지, 최신 main에서 Integration Stage 시작 | `integration.md` |
| Integration Branch에 직접 진입 | CLOSED·closure result·source Commit 재확인 | `repository-entry.md` + `integration.md` |
| Integration 준비 중 main 전진 | 충돌·영향 확인 후 필요한 검증 재수행 | `integration.md` |
| Final Integration PR 중 Work Reopen | 기존 Final PR 병합 금지, 새 Cycle로 복귀 | `integration.md` + `reopen.md` |
| 종료 후 실제 사용에서 문제 발견 | 같은 Work ID로 재개 | `reopen.md` |
| 방법을 모르지만 현재 설계는 명확 | 추가 Reference 필요 여부 확인 | `reference-lookup.md` |
| 저장소에 현재 할 일이 없음 | Final Review 후보 확인 후 없으면 사용자에게 다음 Work 요청 | `work-root.md` |
| 운영 규칙을 수정함 | 영향도와 자체 리뷰 수행 | `rule-maintenance.md` |
