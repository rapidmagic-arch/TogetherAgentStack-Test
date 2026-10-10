# Action Completion Contract

Agent가 한 단계의 작업을 끝냈다고 보고하려면 다음 네 영역이 필요한 경우 모두 완료되어야 한다.

1. `Artifact`: 코드·설계·Review·결정 등 실제 결과물이 저장되어야 한다.
2. `Record`: 결과와 근거가 현재 Task 또는 Issue Thread에 기록되어야 한다.
3. `Projection`: STATUS와 TASK-INDEX가 실제 원본 기록과 일치하도록 갱신되어야 한다.
4. `Delivery`: 다음 Actor가 원격 저장소만 보고 이어갈 수 있도록 필요한 Commit/Push가 완료되어야 한다.

## P1 MUST — 화면 출력은 전달이 아니다

Agent가 질문·진행 결과·중단 이유를 사용자 화면에 출력했더라도 공용 Work Branch에 기록·마킹·Push하지 않았다면 다른 Agent에게 작업을 전달한 것으로 인정하지 않는다.

## P1 MUST — 원격 변경 덮어쓰기 금지

Agent가 Work Branch를 읽은 이후 원격 Head가 변경되었으면 자신이 읽은 과거 상태를 강제로 Push하지 않고 최신 Task·Thread·STATUS를 다시 읽어 변경을 합친 뒤 기록한다.

## P1 MUST — 실패도 기록한다

시도한 방법이 실패하여 실제 산출물이 바뀌지 않았더라도 그 실패가 다음 판단에 영향을 주면 Task 또는 Thread에 시도·결과·관련 Commit을 기록하여 같은 실패를 반복하지 않게 한다.
