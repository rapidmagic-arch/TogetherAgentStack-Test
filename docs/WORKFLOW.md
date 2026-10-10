# Collaboration Workflow Guide

이 문서는 저장소 전체 순환을 한 번에 이해하기 위한 설명 Guide이며 정확한 상태·역할·경로·Git Review 경계의 Canonical 정의는 `rules/contracts/`를 따른다.

## 1. 전체 순환

```text
[Repository Entry]
   ├─ main/work/design/impl ───────────────► [WORK_DISCOVERY]
   ├─ integrate/<WORK-ID> ────────────────► [INTEGRATION]
   └─ Maintenance Branch ─────────────────► [Rule Maintenance]

[WORK_DISCOVERY]
   STATUS + TASK-INDEX + next_actor + open_issue + last record 확인
   ├─ 설계/구현/수정 실행 ────────────────► [EXECUTION]
   ├─ 열린 Issue의 Actor 판단 ───────────► [ISSUE_HANDOFF]
   ├─ Result Review 대기 ─────────────────► [TASK_REVIEW]
   ├─ HUMAN 판단 필요 ────────────────────► [HUMAN_DECISION]
   └─ 필수 Task 없음 ─────────────────────► [FINAL_REVIEW]

[EXECUTION]
   ├─ 같은 Task 계속 ─────────────────────► [EXECUTION]
   ├─ 다른 Actor 판단 ────────────────────► [ISSUE_HANDOFF]
   ├─ Result 준비 ────────────────────────► [TASK_REVIEW]
   └─ HUMAN 전용 판단 ────────────────────► [HUMAN_DECISION]

[ISSUE_HANDOFF]
   Question → Decision → 반영 → Verification → Confirm → CLOSE.md
   ├─ 실행 더 필요 ───────────────────────► [EXECUTION]
   ├─ Review 가능 ────────────────────────► [TASK_REVIEW]
   └─ HUMAN 판단 남음 ───────────────────► [HUMAN_DECISION]

[TASK_REVIEW]
   Review 범위 = review_base_commit..reviewed_commit
   ├─ PASS ───────────────────────────────► [PRIORITY_REFRESH]
   ├─ REWORK ─────────────────────────────► [EXECUTION]
   ├─ DESIGN_ISSUE ───────────────────────► [ISSUE_HANDOFF]
   └─ USER_DECISION_REQUIRED ─────────────► [HUMAN_DECISION]

[PRIORITY_REFRESH]
   ├─ 다음 Task ──────────────────────────► [EXECUTION]
   ├─ 필수 Task 없음 ─────────────────────► [FINAL_REVIEW]
   └─ HUMAN 판단 필요 ────────────────────► [HUMAN_DECISION]

[FINAL_REVIEW] ───────────────────────────► [HUMAN_DECISION]

[HUMAN_DECISION]
   추가 HUMAN 응답이 필요한 경우에만 next_actor=HUMAN / 필요 시 WAITING
   이미 충분한 사용자 결정이 있으면 대기 없이 즉시 적용
   ├─ Work 재탐색 ────────────────────────► [WORK_DISCOVERY]
   ├─ 실행·수정 ─────────────────────────► [EXECUTION]
   ├─ Issue/설계 판단 적용 ──────────────► [ISSUE_HANDOFF]
   ├─ Review 재개 ────────────────────────► [TASK_REVIEW]
   ├─ Priority 결정 ─────────────────────► [PRIORITY_REFRESH]
   ├─ 전체 재검토 ───────────────────────► [FINAL_REVIEW]
   └─ CLOSED/COMPLETE 또는 INCOMPLETE ───► [INTEGRATION]

[INTEGRATION]   (Work State는 CLOSED 유지)
   최신 main → integrate/<WORK-ID> → 승인된 최종 산출물만 선별
   → Final Integration PR → CLOSED/closure/source SHA 재확인
   ├─ 정상 ───────────────────────────────► main
   └─ Reopen 또는 source 변경 ───────────► [REOPEN]

[REOPEN]
   ├─ 새 Task 탐색 ──────────────────────► [WORK_DISCOVERY]
   ├─ 실행 ──────────────────────────────► [EXECUTION]
   ├─ 특정 Task 재Review ────────────────► [TASK_REVIEW]
   └─ Work 전체 재Review ────────────────► [FINAL_REVIEW]
```

## 2. Stage와 Work State는 다르다

Lifecycle Stage는 Agent가 지금 어떤 절차를 수행하는지 설명하고 Work State는 Work 전체가 진행·대기·리뷰·종료 중 어디에 있는지 표시한다. `HUMAN_DECISION`과 `INTEGRATION`은 새 Work State가 아니며 HUMAN 판단만 남은 경우에는 기존 `WAITING`, 사용자 종료 승인 뒤 Integration 중에는 기존 `CLOSED`를 유지한다.

## 3. HUMAN 판단은 어디서든 같은 방식으로 처리한다

Review의 `USER_DECISION_REQUIRED`, Issue의 사용자 전용 판단, Priority 선택, Final Review 종료 판단뿐 아니라 사용자가 진행 중인 Cycle을 즉시 종료하겠다고 명시한 경우에도 HUMAN_DECISION을 사용한다. HUMAN의 추가 응답이 필요한 경우에는 판단 질문·선택지·영향·적용 대상·응답 후 재개 지점을 Work에 기록하고 `next_actor=HUMAN`으로 표시한다. 사용자가 이미 충분히 명확한 결정을 제공한 경우에는 같은 결정을 다시 묻지 않고 기록한 뒤 해당 재개 Stage 또는 INTEGRATION으로 즉시 이동한다.

## 4. PR은 무엇을 대체하고 무엇을 대체하지 않는가

GitHub PR은 파일 Diff, inline comment, Review, CI/Check처럼 Git 변경분 검토에 이미 존재하는 기능을 재사용하는 Review Surface이다. PR은 Work Root, Task, Issue Thread, `next_actor`, 사용자 종료 권한을 대체하지 않는다.

Task Review가 승인하는 범위는 `review_base_commit..reviewed_commit`으로 고정하고 PR의 현재 Head나 Approve 표시만으로 PASS를 확정하지 않는다. 같은 Task가 REWORK로 돌아가면 review_base_commit을 유지하고 reviewed_commit을 새 Result Commit으로 전진시켜 전체 Task 변경 범위를 다시 확인한다. Task의 일반 Base Commit은 Task 입력 기준점이고 Review Base Commit은 승인할 전체 변경 범위의 시작점이므로 두 값을 자동으로 동일시하지 않는다.

## 5. Review Surface PR과 Final Integration PR

`design/<WORK-ID>`와 `impl/<WORK-ID>`의 PR은 진행 중 변경을 보기 위한 Review Surface이므로 가능하면 Draft로 유지하고 Work 진행 중 main에 병합하지 않는다. 사용자 종료 승인 후에는 당시 최신 main에서 `integrate/<WORK-ID>`를 새로 만들고 승인된 최종 산출물만 적용한 Final Integration PR을 main 대상으로 생성한다.

특정 Work와 무관한 저장소 규칙·문서·기반 구조 유지보수는 일반 Maintenance PR을 사용할 수 있으며 Work 결과를 다루기 시작하면 Work Canonical과 Human Gate를 우회해서는 안 된다.

## 6. 상태를 얼마나 사용하는가

Work Root의 상위 상태만 `진행(PROGRESS) / 대기(WAITING) / 리뷰(REVIEW) / 종료(CLOSED)`로 관리한다. Task와 Issue는 진행 단계를 여러 상태 코드로 나누지 않고 마지막 기록, `next_actor`, `condition`, Review 결과, 완료 시점으로 현재 상황을 설명한다.

## 7. 무엇이 어디에 있는가

| 영역 | 무엇을 보관하는가 | 무엇을 보관하지 않는가 |
|---|---|---|
| `main` | 현재 유효한 규칙, 승인된 Design, 검증된 최종 Project 결과 | Thread 전문, 시행착오, STATUS, Task Priority |
| `work/<WORK-ID>` | Task, Issue Thread, STATUS, TASK-INDEX, Handoff, Canonical Review 판정 | 최종 제품 자체의 작업 원본 |
| `design/<WORK-ID>` | 진행 중 Design 산출물 | 공용 Thread 원본 |
| `impl/<WORK-ID>` | 실제 코드·설정·테스트 Sandbox | 공용 Thread 원본 |
| Review Surface PR | Diff, inline discussion, Review/Check 증거 | Work 상태, Task Canonical 판정, 사용자 종료 승인 |
| `integrate/<WORK-ID>` | 최신 main 위에 조립한 최종 반영 후보 | Work 과정 기록 |
| Final Integration PR | 최종 main Diff와 Merge 전 Review/Check | Work 종료 결정 자체 |
| Maintenance PR | 특정 Work와 무관한 저장소 규칙·기반 구조 변경 | Work의 사용자 종료 승인 우회 |
| `references/` | 필요할 때 선택적으로 읽는 외부 방법론 Reference | 현재 Task, 프로젝트 명령, 종료 권한 |

## 8. Task를 언제 나누는가

현재 Task를 완료하기 위한 Condition·Method 변경, 오류 수정, 테스트 추가, 같은 Module의 세부 구현은 기존 Task 안에서 처리한다. 독립 Module·Component·기능 책임·상위 구조처럼 별도의 결과와 검증 기준을 가질 수 있는 일이 생기면 새로운 Task로 분리한다.

## 9. Thread를 언제 닫고 어디로 돌아가는가

Issue Thread는 답변이 왔거나 PR comment가 Resolve됐을 때가 아니라 `최종 결정 → 실제 반영 → 검증 → 관련 Actor 확인 → Close Summary`가 모두 끝났을 때 닫는다. 닫힌 뒤 추가 실행이 필요하면 EXECUTION, 결과가 Review 가능하면 TASK_REVIEW, HUMAN 전용 판단이 남으면 HUMAN_DECISION으로 이동한다.

## 10. Work를 언제 닫고 다시 여는가

Agent는 실제 조건에 따라 진행·대기·리뷰를 갱신할 수 있지만 Work Root를 종료로 만들고 완성 또는 미완성을 확정하는 권한은 사용자에게만 있다. 사용자는 Final Review 이후뿐 아니라 진행 중 Cycle을 즉시 미완성 종료할 수 있으며 이 경우 남은 항목을 현재 근거로 명시한 뒤 HUMAN_DECISION에서 종료 결과를 확정한다. Final Integration PR의 Merge는 이미 내려진 사용자 종료 결정을 전달하는 단계이며 종료 승인 자체가 아니다.

Final Integration PR이 열려 있더라도 Work가 Reopen되거나 source 결과가 달라지면 기존 PR을 병합하지 않고 새 Cycle로 돌아간다. 재개 후 실행이 먼저면 PROGRESS, 전체 Review가 먼저면 REVIEW로 매핑한다.

## 11. Runtime 자동화 경계

이 Workflow는 Agent가 따라야 할 계약을 설명하지만 Writer와 Watcher가 이미 자동 구현되었다는 뜻은 아니다. Repository 또는 Hermes Runtime에서 실제 자동화가 검증되기 전에는 Handoff 기록·STATUS 갱신·PR 참조·Commit/Push와 변경 감지를 자동 실행된 것으로 가정하지 않고 `docs/RUNTIME-CAPABILITIES.md`에서 현재 구현 상태를 확인한다.

## 12. Reference는 언제 보는가

Agent는 Repository Rule·현재 Design·Task만으로 판단할 수 있는지 먼저 확인하고 설계 방법론·코딩 원칙·검증 전략처럼 추가 지식이 필요한 경우에만 `references/`에서 관련 Topic을 선택적으로 조회한다.
