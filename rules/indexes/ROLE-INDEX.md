# Role Index

| Role | 최초 확인 | 주 작업 | 넘겨야 하는 대표 상황 |
|---|---|---|---|
| HUMAN | Final Report 또는 사용자 판단 요청 | 목적·권한·종료 결과 승인 | 승인 후 다음 Actor가 명확해짐 |
| DESIGNER | STATUS의 Designer 대기 Issue | Design 작성·Issue Decision | 구현 가능하면 IMPLEMENTER, 사용자 전용 결정이면 HUMAN |
| IMPLEMENTER | 현재 Task·Design Ref·Sandbox | 구현·테스트·자체 오류 해결 | 설계 판단이면 DESIGNER, Review 가능하면 REVIEWER |
| REVIEWER | Task·Design·Result Commit·검증 | PASS/REWORK/DESIGN_ISSUE/USER_DECISION_REQUIRED 판정 | 판정 결과에 따라 IMPLEMENTER, DESIGNER, HUMAN 또는 다음 Task로 이동 |

main 통합은 별도 전용 Role이 아니라 사용자 종료 승인 이후 Integration Manual을 맡은 Agent의 절차이며, 이 절차가 HUMAN의 승인 권한을 대신하지 않는다.

한 Agent가 여러 Role을 수행하더라도 각 행동은 현재 Role의 권한과 Manual을 명시적으로 적용한다.
