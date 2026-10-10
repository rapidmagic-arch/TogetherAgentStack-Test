# Pull Request

## Purpose

- [ ] 이 PR은 진행 중 Work 변경을 검토하는 Review Surface이며 main에 병합하지 않는다.
- [ ] 이 PR은 사용자 Work 종료 승인 후 생성된 Final Integration PR이다.
- [ ] 이 PR은 특정 Work 결과 전달과 무관한 Repository Maintenance 변경이다.

위 세 항목 중 현재 PR의 목적에 해당하는 하나만 선택한다. Maintenance PR이 특정 Work 결과를 다루기 시작하면 Work 규칙과 Human Gate를 우선 적용한다.

## Work

- Work ID: `<WORK-ID or NOT_APPLICABLE>`
- Related Task(s): `<TASK-ID or NOT_APPLICABLE>`
- Source Design Commit: `<sha or NOT_APPLICABLE>`
- Source Implementation Commit: `<sha or NOT_APPLICABLE>`

## Review Target

- Review Base Commit: `<sha or NOT_APPLICABLE>`
- Reviewed Commit / Exact Head: `<sha>`
- Review Range: `<review_base_commit..reviewed_commit or NOT_APPLICABLE>`
- Verification: `<tests, checks, inspection, or evidence>`
- Known Limits: `<limits or none>`

## Final Integration Only

- Human closure result: `<COMPLETE|INCOMPLETE|NOT_APPLICABLE>`
- Base main commit: `<sha or NOT_APPLICABLE>`
- Excluded process records checked: `<yes/no/NOT_APPLICABLE>`

## Boundary

PR Review는 Work/Task의 Canonical 판정이나 사용자 종료 승인을 대신하지 않는다. Review Surface PR은 main에 병합하지 않고 Final Integration PR만 사용자 종료 승인 이후 Work 결과를 main에 전달하는 데 사용하며, Maintenance PR은 특정 Work 결과를 우회 통합하는 경로로 사용하지 않는다.
