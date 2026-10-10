# Runtime Capabilities

이 문서는 저장소 규칙이 요구하는 행동과 실제 Runtime 자동화 구현 상태를 구분하여 Agent가 규칙에 적혀 있다는 이유만으로 자동 기능이 이미 존재한다고 추론하지 않게 한다.

## GitHub PR / Review

- 활용 범위: Diff, inline comment, Review submission, PR conversation, CI/Check와 최종 Merge 같은 GitHub 네이티브 기능은 연결된 Runtime이 해당 권한을 제공할 때 재사용할 수 있다.
- Canonical 경계: PR은 Review Surface와 전달 증거이며 Work/Task/Issue/사용자 종료 권한의 Canonical이 아니다.
- 이벤트 한계: PR에 comment나 Review가 추가됐다는 사실만으로 Hermes 또는 다른 Agent가 자동 실행된다고 가정하지 않는다.
- 보호 규칙 한계: Branch protection, Required Review, Required Check는 실제 Repository 설정에서 활성화가 확인된 경우에만 물리적 Gate이다.
- Identity 한계: 같은 GitHub 사용자·App·Bot이 PR 생성과 Review를 모두 수행할 수 있으므로 GitHub 승인 표시만으로 독립 Actor Review나 HUMAN 승인을 추론하지 않는다.

## Writer

- 요구 행동: Agent가 Handoff 시 Task/Issue 기록, STATUS·TASK-INDEX 갱신, Commit/Push와 필요 시 PR 참조 기록까지 완료해야 한다.
- 현재 규칙 상태: 행동 계약은 정의되어 있다.
- 자동 구현 상태: 현재 Repository에는 전용 Writer 프로그램이 구현되어 있지 않다.
- 조사 상태: Hermes 네이티브 Git/Workflow/PR 기능으로 별도 프로그램 없이 충족 가능한지 외부 조사 중이다.

## Watcher

- 요구 행동: 원격 Repository의 Work 기록과 필요 시 PR Review 변화에서 자신의 `next_actor` 또는 새 작업을 발견할 수 있어야 한다.
- 현재 규칙 상태: Repository Entry와 Handoff 계약은 정의되어 있으나 자동 감시 주기는 운영 규칙으로 확정하지 않았다.
- 자동 구현 상태: 현재 Repository에는 전용 Watcher/Poller/Scheduler 프로그램이 구현되어 있지 않다.
- 조사 상태: Hermes 네이티브 Scheduler/Trigger 기능과 GitHub 상태 조회를 조합해 충족 가능한지 외부 조사 중이다.

## MUST — 해석 경계

Writer나 Watcher의 자동 구현이 검증되기 전에는 Agent가 자동 실행된다고 가정하지 않으며, GitHub notification도 자동 Agent 호출과 동일시하지 않는다. 네이티브 기능 검증 또는 실제 코드 구현이 끝난 뒤 이 문서와 관련 Manual을 함께 갱신한다.
