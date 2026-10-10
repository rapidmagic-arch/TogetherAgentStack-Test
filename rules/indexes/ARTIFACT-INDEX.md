# Artifact Index

| Artifact | Canonical 위치 | 읽는 이유 | 수정 시점 |
|---|---|---|---|
| WORK ROOT | `work/<WORK-ID>/WORK-ROOT.md` | 불변 목적·범위와 종료/재개 역사를 확인 | Work 생성, 목적/범위의 사용자 승인 변경, 종료/재개 기록 |
| STATUS | `work/<WORK-ID>/STATUS.yaml` | 현재 상태·Next Actor·Issue·우선 Task를 빠르게 찾음 | 의미 있는 행동 종료·Handoff·Work 상태 변경 |
| TASK-INDEX | `work/<WORK-ID>/TASK-INDEX.yaml` | Task 목록·완료 시점·현재 우선순위를 찾음 | Task 생성·완료·우선순위 재평가 |
| TASK | `tasks/<TASK-ID>/TASK.md` | 현재 목적·범위·Condition을 확인 | Task 생성 또는 범위 명시 보완 |
| SUMMARY | `tasks/<TASK-ID>/SUMMARY.md` | 후속 Task가 결과를 빠르게 이해 | 의미 있는 결과 및 Task 완료 시 |
| EVENT | `tasks/<TASK-ID>/events/` 또는 Issue Thread | 의미 있는 요청·진행·질문·결정·결과·Review를 추적 | 필요한 사건이 발생할 때 |
| ISSUE | `issues/<ISSUE-ID>/ISSUE.md` | 다른 Actor 판단이 필요한 현재 문제와 질문을 확인 | Issue 생성 또는 질문 범위가 바뀔 때 |
| ISSUE CLOSE | `issues/<ISSUE-ID>/CLOSE.md` | Thread 최종 결론과 반영을 확인 | Issue 종료 직전 |
| DESIGN ITEM | `design-<WORK-ID>/` | 현재 설계 결정의 작업 원본을 확인 | Designer가 설계 변경을 채택할 때 |
| PROJECT | `project-<WORK-ID>/` | 실제 제품 산출물을 확인 | Implementer가 구현·테스트할 때 |
| FINAL CHECKLIST | `work/<WORK-ID>/FINAL-CHECKLIST.md` | 종료 후보의 전체 정합성을 확인 | 사용자 종료 판단 직전 |
