# Agent Collaboration Workspace

이 저장소는 사람과 여러 에이전트가 하나의 Git 작업 공간에서 설계·구현·검토·검증을 이어가도록 관리하며, 사용자가 에이전트 사이의 메시지를 직접 복사하지 않아도 현재 작업과 다음 행동이 저장소만으로 복원되게 한다.

## Start Here

1. Agent는 `AGENTS.md`를 읽어 저장소 진입 순서를 확인한다.
2. 전체 순환을 먼저 이해해야 하면 `docs/WORKFLOW.md`를 읽는다.
3. 실제 작업에서는 `rules/indexes/MANUAL-INDEX.md`에서 현재 상황에 필요한 Manual만 선택한다.
4. 현재 Work가 있으면 `STATUS.yaml`과 `TASK-INDEX.yaml`을 먼저 확인한다.
5. GitHub PR/Review를 사용할 때는 `rules/contracts/git-review.yaml`을 따라 PR을 Work 원장과 혼동하지 않는다.
6. 추가 방법론이 필요할 때만 `references/` 서브모듈을 선택적으로 참조한다.
7. Writer/Watcher 같은 Runtime 자동화가 실제 구현되어 있다고 가정하지 말고 `docs/RUNTIME-CAPABILITIES.md`에서 현재 상태를 확인한다.

## 핵심 원칙

1. 저장소가 작업의 진입점이며, 에이전트는 과거 대화나 개인 기억보다 저장소의 현재 상태를 먼저 확인한다.
2. `main`은 현재 유효한 규칙·승인된 설계·검증된 결과만 보존하고, 문제 해결 과정 전체는 공용 `work/<WORK-ID>` 브랜치에 남긴다.
3. `work/<WORK-ID>`는 Task·Issue Thread·현재 상태·우선순위·Agent Handoff와 Canonical Review 판정의 원본이다.
4. `design/<WORK-ID>`는 설계 작업용 브랜치이고 `impl/<WORK-ID>`는 실제 구현·테스트용 브랜치이며, 두 브랜치는 Thread의 원본을 따로 만들지 않는다.
5. GitHub Review Surface PR은 Diff·inline comment·Review/Check를 제공하지만 Work 상태·Task 판정·사용자 종료 권한을 대체하지 않고 Work 진행 중 main으로 병합하지 않는다.
6. Work Root의 최종 `종료(CLOSED)/완성(COMPLETE)` 또는 `종료(CLOSED)/미완성(INCOMPLETE)`은 사용자 승인으로만 확정한다.
7. 사용자 종료 승인 후에는 당시 최신 main에서 `integrate/<WORK-ID>`를 만들고 승인된 최종 산출물만 Final Integration PR로 main에 전달한다.
8. `project-<WORK-ID>/`는 실제 제품 구조를 유지하는 Sandbox이며 Task 번호를 제품 폴더 구조로 사용하지 않는다.
9. `references/`는 추가 판단 근거가 필요할 때만 선택적으로 읽는 외부 Reference 서브모듈이다.

모든 규칙 문장은 해당 문장만 읽어도 적용 대상·조건·행동·결과가 이해되도록 작성하며 공통 코드와 상태값은 `rules/contracts/`에서만 Canonical로 정의한다.
