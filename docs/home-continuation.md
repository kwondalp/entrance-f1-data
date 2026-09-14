# 집 PC에서 이어서 하기

세 저장소 전체 재개 절차는 Tools의 `docs/home-continuation.md`를 먼저 읽는다. 각 저장소의 PROJECT_RULES → AGENTS → AI_HANDOFF → HUMAN_HANDOFF와 실제 Git 상태를 확인한다. 같은 이름의 기존 개발 브랜치가 있어도 로컬 변경·stash·원격 이후 변경을 먼저 비교한다. 현재 Git 상태를 이 문서의 과거 사실로 대신하지 않는다.

운영 core는 2026-09-13 Spanish GP Race까지 실제 발행됐다. Driver 23명, Constructor 11명 전체 순위와 포인트, Race 22행, Wins 116행 및 해시를 운영 브라우저에서 대조했다. 이후 동일 입력 no-op과 실제 예약 run [34819909414](https://github.com/kwondalp/entrance-f1-data-tools/actions/runs/34819909414)이 성공했다. Tools의 `docs/recovery-evidence/20260914/`에 이 시점의 공개 JSON 검증과 화면을 보존했다. 이 인원수·경기 수를 미래 live 데이터에 강제하지 않는다.

개발 자료는 최신 운영 core와 7개 immutable current 파일의 바인딩을 동기화했다. 과거 프로필 사실은 2026-09-06 원문 근거를 유지하고, Results·Stats는 2026-09-13 기준을 별도로 검증한다. 기존 shared-driver backfill 수정은 1,864개 조합이며 기존 2026-08-23 coverage를 유지한다. 운영 승격은 아직 대기다.

Git으로 받을 수 있는 연구 자료:

- `research/power-strength/v2/releases/strength-2026-1332b18bde041da18a75`: R13/R14 race-seed 재생을 반영한 R14 연구 묶음. 예선 98/260로 50% gate 미달, 선택 모델 없음.
- `research/value-recovery/v1/value-9df8a1a94cf7c56e5e159d0d`: 23명 공식 포인트와 비용 대조 및 같은 입력 no-op 완료. 최신 제안 지문은 해당 상위 README 참조.

이 경로들은 공개 소비용 포인터가 아니다. 운영 Power·Value manifest와 Value 정책은 그대로 보존했다. 원본이 없는 프로필 사실이나 나이 기록은 보충하지 않는다. 연구 원문 timing/cache는 Git에 포함되지 않으며, 재생 시 Tools의 검증된 수집 경로로 확보한다. 새 데이터는 Tools 생성·검증과 기존 Data-last 정상 발행 계약을 따른다. Web 파일에서 통계를 직접 고치지 않는다.
