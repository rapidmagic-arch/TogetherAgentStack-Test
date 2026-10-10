# Manual Index

이 Index는 Agent가 모든 문서를 읽지 않고 현재 상황에 필요한 Manual만 찾도록 하는 Router이다.

| 현재 상황 | MUST로 읽을 Manual | 확인할 현재 입력 | 완료 후 기대 결과 |
|---|---|---|---|
| 저장소 최초 진입 | `repository-entry.md` | Branch, Head, Work 존재 여부 | 현재 역할·Work·Integration·Maintenance 중 현재 작업면 식별 |
| Work Root 진입/생성 | `work-root.md` + `branching.md` | STATUS, TASK-INDEX, base main commit | 현재 Work 상태와 역할 브랜치 기준 식별 |
| Task 신규/계속 판단 | `task.md` | Task 목적, Condition, 이전 Summary | 같은 Task 유지 또는 새 Task 결정 |
| Designer 작업 | `design.md` | 자신을 기다리는 Issue, Task, Design Commit, 필요 시 Review Surface PR | 설계 Decision과 적용 Commit 기록 |
| Implementer 작업 | `implementation.md` | Task, active Design Commit, Sandbox, Review Surface PR | 구현·테스트 결과 또는 Issue Handoff |
| Reviewer 작업 | `review.md` + `rules/contracts/git-review.yaml` | Task, Design Commit, review_base_commit, reviewed_commit, PR Diff/Review 증거 | 정확한 변경 범위에 대한 PASS/REWORK/DESIGN_ISSUE/USER_DECISION_REQUIRED 판정 |
| 다른 Actor에게 넘김 | `handoff.md` + `status-marking.md` | Issue/Task, next_actor, Commit, 관련 PR | Work 기록·마킹·Push 완료 |
| HUMAN 판단 필요 | `handoff.md` + `status-marking.md` + 판단을 발생시킨 원래 Manual | 질문 또는 이미 주어진 사용자 결정, 영향, 적용 Task/Issue, 응답 후 재개 지점 | 추가 응답이 필요하면 next_actor=HUMAN, 이미 결정이 충분하면 실제 재개 Stage로 즉시 이동 |
| STATUS/우선순위 최신화 | `status-marking.md` | Task/Issue 원본, Last/Next Actor | Projection이 실제 작업과 일치 |
| Issue Thread 처리 | `thread.md` | Issue, 관련 Task, 마지막 Message, 필요 시 PR thread | Decision 반영·검증·Close 후 EXECUTION/TASK_REVIEW/HUMAN 판단 중 실제 다음 단계로 복귀 |
| Branch 사이 결과 전달 | `branching.md` | design/impl commit, work Task, PR 참조 | 명시적 SHA로 다음 Actor 기준 고정 |
| 전체 마무리 | `final-review.md` | 모든 필수 Task, Issue, Verification | 사용자 종료 판단용 보고 준비 |
| 사용자 종료 승인 후 main 반영 | `integration.md` + `rules/contracts/git-review.yaml` | 최신 main, 종료 결과, source Commit, 최종 산출물 | Integration Branch와 Final Integration PR로 최종 결과만 main에 전달 |
| 종료 후 재개 | `reopen.md` | 이전 종료 기록, 재개 이유 | 같은 Work ID로 PROGRESS 또는 REVIEW Cycle 시작 |
| 방법론 추가 필요 | `reference-lookup.md` | 현재 질문, 기존 Rule/Design | 관련 Reference를 채택하거나 필요한 Reference를 명시해 요청 |
| 규칙 자체 수정 | `rule-maintenance.md` | 변경 목적, 영향 Contract/Manual | 영향도 검토·자체 리뷰가 끝난 규칙 변경 |

## MUST — 선택 로딩

Agent는 현재 역할과 상황에 필요한 Manual을 반드시 읽되 관련 없는 Manual 전체를 관성적으로 로딩하여 현재 Task 판단을 흐리지 않는다.
