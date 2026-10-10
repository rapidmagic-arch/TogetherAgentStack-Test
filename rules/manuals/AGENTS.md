# Manuals Router

`rules/manuals/`는 현재 상황에서 Agent가 실제로 무엇을 해야 하는지를 설명하는 행동 매뉴얼 영역이다.

## MUST — Manual 작성 구조

새 Manual 또는 큰 수정은 가능한 범위에서 `목적/정의 → 적용 조건 → MUST → CHECK → 금지 → 완료 조건 → 다음 단계` 순서를 사용하여 한 파일만 읽어도 현재 행동의 입구와 출구를 판단할 수 있게 한다.

## MUST — Contract 참조

Role·Work State·Review Result·ID·Branch·Path·Message Type을 Manual에서 독립적인 새 의미로 정의하지 않고 `rules/contracts/`의 Canonical 의미를 사용한다.

## CHECK — 중복

같은 상황을 두 Manual이 서로 다른 절차로 지시하지 않는지 확인하고, 공통 절차는 한 Manual에 소유권을 주고 다른 Manual에서는 링크와 적용 조건만 설명한다.
