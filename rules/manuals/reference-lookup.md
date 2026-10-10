# Reference Lookup Manual

## 정의

`references/`는 Agent가 현재 Repository Rule·Design·Task만으로 판단하기 어려운 방법론을 보강할 때 사용하는 외부 Reference 서브모듈이며 작업을 지시하는 Inbox나 Lifecycle 원장이 아니다.

## CHECK — 조회 필요성

현재 질문이 Repository Rule, 현재 Design, 이전 Task Summary만으로 충분히 해결 가능한지 먼저 확인하고 추가 방법론·설계 원칙·코딩 원칙·검증 전략이 필요한 경우에만 Reference를 조회한다.

## MUST — Submodule 가용성 확인

`references/`가 비어 있거나 읽을 수 없을 때 이를 Reference가 존재하지 않는 것으로 단정하지 않고 서브모듈 초기화 여부를 확인한다. 부모 저장소는 특정 Reference Commit을 고정하므로 명시적인 Reference 업데이트 작업 없이 원격 `main` 최신 Commit으로 자동 전진시키지 않는다.

## MUST — 선택적 로딩

Reference 저장소 전체를 기본 Context로 로딩하지 않고 현재 질문과 직접 관련된 Topic만 찾아 읽는다.

## MUST — 채택과 조회 구분

Reference를 읽었다는 사실만으로 현재 프로젝트 설계가 되지 않으며 실제 채택한 원칙만 Design 또는 Task에 적용 범위와 함께 기록한다.

## CHECK — 버전 추적

Reference의 특정 판단이 Design 또는 Review 결론에 중요한 영향을 주면 Topic과 서브모듈 Commit을 함께 기록하여 나중에 어떤 기준을 보았는지 재현할 수 있게 한다.

## MUST — Reference 부재

필요한 Topic이 없고 그 부재 때문에 현재 판단을 안전하게 완료할 수 없으면 즉석에서 Canonical Reference를 꾸며내지 않고 필요한 Reference가 무엇인지 사용자 또는 별도 Reference 작업에 요청한다.
