# Canonical Ownership

- `rules/contracts/`는 공통 코드·상태·ID·역할·경로·브랜치·Message Type의 Canonical이다.
- `main`은 현재 유효한 규칙·승인된 설계·검증된 최종 결과의 Canonical이다.
- `work/<WORK-ID>`는 Task·Issue Thread·STATUS·Task Priority·Handoff 과정의 Canonical이다.
- `design/<WORK-ID>`는 진행 중 설계 산출물의 작업 원본이며, 승인되어 main에 반영된 이후에는 main의 버전이 현재 유효 기준이 된다.
- `impl/<WORK-ID>`는 구현·테스트 작업용 브랜치이며, 실제 제품 파일은 `project-<WORK-ID>/`의 제품 구조를 유지한다.
- `references/`는 외부 Reference의 고정 Commit을 가리키는 서브모듈이며 프로젝트 명령·Task·설계의 Canonical이 아니다.

## P0 MUST — 충돌 처리

같은 정보가 여러 위치에서 서로 다르면 위 Canonical 소유권을 기준으로 현재 유효값을 결정하고, 비Canonical 복사본을 근거로 상태·권한·범위를 변경하지 않는다.
