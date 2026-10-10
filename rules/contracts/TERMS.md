# Canonical Terms

이 문서는 저장소 운영에서 일반 의미보다 좁거나 특별한 의미로 사용하는 용어를 한곳에서 정의하며, 다른 문서는 동일 용어를 다른 의미로 재정의하지 않는다.

| 용어 | 정의 |
|---|---|
| **Work Root** | 하나의 최초 아이디어가 설계·Task·구현·검증·종료·재개를 거치는 전체 작업 계보이며 하나의 불변 Work ID로 식별한다. |
| **Work ID** | Work Root를 다른 Work Root와 구분하는 `YYMMDD-<topic>-<uuid>` 형식의 불변 식별자이다. |
| **Actor** | 현재 하나의 행동을 특정 Role 권한으로 수행하는 사람 또는 Agent이며, 같은 Agent가 여러 Role을 가질 수 있어도 현재 행동의 Role은 하나로 명확해야 한다. |
| **Role** | HUMAN, DESIGNER, IMPLEMENTER, REVIEWER처럼 어떤 판단과 행동을 할 수 있는지 정하는 권한 책임 단위이다. |
| **Task** | 현재 Work에서 독립적으로 목적과 Verification 결과를 가질 수 있는 실제 수행 기본 단위이다. |
| **Condition** | Task가 성공했다고 판정하기 위해 충족되어야 하는 관찰 가능 조건 또는 판단 기준이다. |
| **Method** | Task의 목적과 Condition을 충족하기 위해 선택하는 구현 방법이며 목적을 바꾸지 않는 범위에서는 Implementer가 변경할 수 있다. |
| **Task Thread** | 하나의 Task가 생성되어 진행·질문·결정·결과·Review를 거치는 전체 작업 기록 계보이다. |
| **Issue Thread** | Task 수행 중 하나의 특정 판단 문제를 여러 Actor가 해결하기 위해 사용하는 하위 대화 단위이다. |
| **Handoff** | 현재 Actor가 필요한 기록·Projection·Commit/Push를 완료하여 다음 Actor가 별도 메시지 복사 없이 저장소만 보고 작업을 이어갈 수 있게 책임을 넘기는 과정이다. |
| **Canonical** | 같은 정보가 여러 위치에 보이더라도 현재 유효한 공식 원본으로 판단하도록 소유권이 지정된 단일 기준 위치이다. |
| **Projection** | Task·Thread·Git 이력 같은 원본을 빠르게 읽기 위해 현재 상태만 요약한 파생 정보이며 원본과 충돌하면 원본을 기준으로 다시 계산한다. |
| **Reference** | 현재 프로젝트의 명령이나 확정 설계가 아니라 여러 작업에서 재사용할 수 있도록 조사·검증된 방법론과 판단 근거이다. |
| **Sandbox** | `project-<WORK-ID>/` 아래에서 실제 코드·설정·테스트·제품 결과를 만드는 구현 작업 영역이다. |
| **Design Item** | 같은 Work Root 안에서 하나의 설계 결정 또는 설계 문제를 현재형으로 설명하는 식별 가능한 설계 문서 단위이다. |
| **Base Commit** | Work 또는 Task가 판단과 구현을 시작할 때 기준으로 삼은 Git Commit이며 이후 변경과 stale 여부를 추적하는 기준점이다. |
| **Result Commit** | Design 또는 Implementation 행동으로 실제 결과가 저장된 Git Commit이며 Work Thread의 Handoff가 이 Commit을 명시적으로 참조한다. |
| **Final Checklist** | 개별 Task 결과 이후 Work 전체의 Design·구현·검증·미완료 항목을 종료 직전에 다시 확인하는 통합 점검이며 사용자 종료 승인을 대신하지 않는다. |
| **Reopen** | 과거 CLOSED 상태를 삭제하지 않고 같은 Work ID에 새로운 작업 Cycle을 추가하여 다시 진행하는 행위이다. |
| **UNKNOWN** | 필수 값이 아직 확인되지 않았음을 명시하는 표기이며 Agent가 임의 값으로 채워서는 안 된다. |
| **NOT_APPLICABLE** | 해당 필드나 조건이 현재 대상에 적용되지 않음을 명시하는 표기이며 단순 미확인과 구분한다. |
