# Documentation Router

`docs/`는 사람이 전체 구조와 프로세스를 빠르게 이해하도록 설명하는 Guide 영역이며 공통 코드·상태·권한의 Canonical을 새로 정의하지 않는다.

## MUST

설명 문서의 상태·Role·경로·Branch 이름이 `rules/contracts/`와 다르면 Contract를 우선하고 설명 문서를 수정한다.

Workflow가 바뀌면 `docs/WORKFLOW.md`, `rules/contracts/lifecycle.yaml`, `rules/indexes/MANUAL-INDEX.md`의 연결이 서로 일치하는지 확인한다.

Runtime 자동화 구현 상태가 바뀌면 `docs/RUNTIME-CAPABILITIES.md`를 갱신하며, 조사 중인 기능을 이미 구현된 기능처럼 표현하지 않는다.
