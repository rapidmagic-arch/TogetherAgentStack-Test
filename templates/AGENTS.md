# Template Router

Template은 규칙 자체가 아니라 새 Work·Task·Issue·Design을 생성할 때 Canonical Contract가 요구하는 필수 정보를 빠뜨리지 않도록 제공하는 시작 골격이다.

## MUST

Template을 사용할 때 Placeholder를 남긴 채 작업 완료로 처리하지 않고 현재 상황에서 필요한 필드를 실제 값으로 채운다.

필수 값을 아직 확인할 수 없으면 `rules/contracts/TERMS.md`의 `UNKNOWN`을 사용하고 임의 추론하지 않으며, 규칙상 현재 대상에 적용되지 않는 필드는 `NOT_APPLICABLE`을 사용하여 단순 미확인과 구분한다.

Template 필드를 추가·삭제할 때는 `rules/contracts/artifacts.yaml`, 관련 Manual, `rules/contracts/paths.yaml`과의 정합성을 함께 확인한다.

기본 Design Template이 특정 설계에 부적합하면 특수 구조를 사용할 수 있으나 목적·범위·결정·검증 기준·미확정 사항은 유지한다.
