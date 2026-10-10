# Rule Group Index

이 Index는 규칙의 주제별 소유권과 기본 우선순위를 연결하며 강제 수준은 각 규칙의 MUST/CHECK/MAY 표기를 따른다.

| 그룹 | 기본 우선순위 | Canonical / Manual | 담당 의미 |
|---|---:|---|---|
| Authority / Canonical / User Gate | P0 | `rules/core/authority.md`, `canonical.md` | 누가 무엇을 확정할 수 있는가 |
| Definitions / Codes | P0 | `rules/contracts/` | ID·Role·Work State·Review Result·Term·Branch·Path의 단일 의미 |
| Entry / Lifecycle / Work | P1 | `repository-entry.md`, `work-root.md` | 어디서 시작하고 어느 단계인지 찾는 법 |
| Task / Priority | P1 | `task.md`, `status-marking.md` | 지금 무엇을 할지와 순서를 정하는 법 |
| Thread / Handoff | P1 | `thread.md`, `handoff.md` | Agent 사이 문제 해결과 책임 전달 방식 |
| Branch Collaboration | P1 | `branching.md` | Work/Design/Impl Commit을 연결하는 방식 |
| Design | P2 | `design.md` | 무엇을 만들기로 결정했는가 |
| Implementation | P2 | `implementation.md` | 실제 Sandbox 결과를 만드는 방식 |
| Review / Verification | P2 | `review.md`, `final-review.md` | Task와 Work 결과를 검증하는 방식 |
| Integration | P2 + P0 Gate | `integration.md` | 사용자 승인 후 최종 산출물을 main에 반영하는 방식 |
| Reference | P3 | `reference-lookup.md` | 추가 방법론을 선택적으로 조회하는 방식 |
| Rule Maintenance | P1 + P0 Canonical | `rule-maintenance.md` | 규칙 수정 영향도와 자체 리뷰 방식 |
