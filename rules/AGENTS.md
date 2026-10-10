# Rules Router

`rules/`는 저장소의 운영 계약을 정의하며, 규칙 수정자는 동일 개념을 여러 파일에 독립 정의하지 않고 Canonical 계약과 Manual의 책임을 분리해야 한다.

## MUST — 읽기 순서

1. `core/OPERATING-PRINCIPLES.md`에서 강제 수준과 최상위 원칙을 확인한다.
2. 특별한 의미의 용어가 나오면 `contracts/TERMS.md`를 기준으로 해석한다.
3. Work State와 Role, Review Result처럼 현재 행동을 가르는 공통 값은 해당 `contracts/` 파일을 확인한다.
4. 우선순위 충돌은 `contracts/priorities.yaml`과 `indexes/RULE-GROUP-INDEX.md`를 따른다.
5. 현재 상황의 행동 절차는 `indexes/MANUAL-INDEX.md`에서 해당 Manual을 선택한다.

## MUST — 수정 순서

1. 변경하려는 내용이 공통 코드·상태·Review 결과·역할·경로·브랜치·식별자·용어인지 먼저 판정한다.
2. 공통 정의이면 `rules/contracts/`의 해당 Canonical 파일을 먼저 수정한다.
3. 행동 절차이면 `rules/manuals/`의 해당 Manual을 수정하고 Canonical 정의를 참조한다.
4. 진입 경로나 상황별 선택 방식이 바뀌면 `rules/indexes/`와 관련 `AGENTS.md`의 Router를 함께 검토한다.
5. Template 입력 필드나 산출물이 바뀌면 `templates/`와 `rules/contracts/artifacts.yaml`의 정합성을 확인한다.
6. 변경 후 중복 정의·상충 문장·끊어진 링크·사용되지 않는 상태·Role·Code·저장소명 하드코딩을 자체 검토한다.

## MUST — 규칙 문장 형식

규칙 문장은 적용 주체와 조건, 반드시 해야 할 행동 또는 확인할 판단, 기록되는 결과가 한 문장 또는 바로 이어지는 문맥에서 명확해야 하며 다른 문서를 추측해야만 뜻을 이해할 수 있는 축약형 문장을 금지한다.
