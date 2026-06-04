# DailyApp 대시보드 (관리 디렉토리)

"하루에 앱 하나" **메타 대시보드**의 소스 + 관리 폴더. GitHub Pages로 배포됨.

- **라이브**: https://doonghwi.github.io/dailyapp-dashboard/
- **repo**: github.com/doonghwi/dailyapp-dashboard (이 폴더 = main 브랜치)

## 구성
- `index.html` — 메타 대시보드. **앱 목록 + 실시간 사용량**을 중앙 RTDB `/dailyapp_stats`에서 자동 로드(하드코딩 X) + **함정 로그** + **플러그인/도구 효율** + **방법론 원칙**.
- `<app>.html` — 앱별 빌드로그(지시/수행 타임라인).
- `reports/` — 일회성 리포트/구버전 진행판(progress.html, ranking-review.html 등) 보관.

## 사용량 집계 방식 (자동)
- 각 앱이 열릴 때 `_shared/dailyapp_stats.dart` 헬퍼로 중앙 RTDB `/dailyapp_stats/<appId>`에
  REST PATCH + 서버 increment 핑 → opens 누적(절대 리셋 금지) + 메타데이터 자동 등록.
- 대시보드는 그 노드를 읽어 앱을 자동 나열. 새 앱은 핑 한 번이면 등장.

## 갱신/배포
- 내용 수정 후 이 폴더에서: `git add -A; git commit; git push` (main→Pages 자동 반영).
- 새 앱 추가 시: index.html의 `APPS` 폴백 메타데이터에 한 줄 추가(선택) — 핑만 있어도 자동 표시됨.

## 새 앱 만드는 법
- 표준 워크플로우/프롬프트: `../_make-new-app/WORKFLOW.md`, `../_make-new-app/PROMPT_TEMPLATE.md`
