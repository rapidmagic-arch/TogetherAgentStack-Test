# Work Root `261010-writer-skill-test-46fdf8`

이 Work는 TogetherAgentStack Template의 Writer Skill만 검증하기 위한 1회차 테스트다. 산출물은 의도적으로 단순하게 유지한다.

## 목적

`writer-test.txt` 1개 파일을 Work Lifecycle을 따라 만든 뒤, DESIGNER Handoff가 Writer Skill 절차대로 Work Canonical에 정확히 기록되고 Commit + Push되어 다음 Actor에게 별도 메시지 없이도 작업이 전달되는지 검증한다.

## 검증 범위

- DESIGNER 단계의 Handoff 절차가 Writer Skill 본문에 적힌 13단계와 동일한 결과를 만드는지
- STATUS / TASK-INDEX Projection이 원본 기록과 정합하는지
- `next_actor=IMPLEMENTER`, `active_design_commit` 정확성
- `based_on_work_commit`이 Push 직전 읽은 work HEAD와 일치
- Push 성공, 로컬/원격 work HEAD 일치

## 검증 범위 밖 (1차 한정)

- Watcher / Cron / 자동 Writer 프로그램 / Kanban / Webhook / adapter
- Implementation / Review / Final Review / Integration 단계 (이번 회차는 DESIGNER Handoff까지만)
- Writer Skill 본문 수정, TogetherAgentStack 원본 Template 수정

## base main Commit

`5e8204221d387310bb7ad17e3c0e337a029f662c` (2026-10-10, 첫 Lifecycle Dry-run main merge)

## 종료 조건

이 Work는 `WAITING`에서 종료하지 않고, 첫 테스트의 DESIGNER Handoff Push가 정상 완료되면 그 자체로 충분한 데이터를 얻는다. 후속 테스트(원격 경합, HUMAN Gate)는 별도 절차로 진행한다.