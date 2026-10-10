# Contracts Router

`rules/contracts/`는 여러 Manual이 공통으로 사용하는 ID·Role·Work State·Review Result·Branch·Path·Message Type·Artifact·특수 용어를 한곳에서 정의하는 Canonical 영역이다.

## MUST

- 이미 존재하는 공통 값의 의미를 바꿀 때 새 문서에서 재정의하지 않고 해당 Contract를 먼저 수정한다.
- Contract 변경 후 해당 값을 사용하는 Manual·Index·Template을 검색하여 의미·필드·경로가 일치하는지 검토한다.
- 이미 발급된 ID나 과거 종료·재개 이력을 새 규칙에 맞춘다는 이유로 소급 재작성하지 않는다.
- YAML 값은 Agent가 이름만 보고 추측하지 않도록 `meaning`, `condition`, `rule`, `label`, `next` 중 필요한 설명을 포함한다.
