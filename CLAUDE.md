# TILTED HANNAM bespoke direction

웨딩 고객이 연출 옵션(버진로드, 아치, 테이블, 부케 등)을 단계별로 고르고 PDF로 출력하는 정적 웹페이지. 빌드 도구 없음.

## 파일
- `index.html` — 앱 전체 (CSS, HTML, JS 한 파일). 단계 목록은 `const steps`, 선택값은 `const state`.
- `admin_option_image_map.json` — 옵션별 이미지 URL. 키 형식은 `stateKey|value` (예: `gardenRoadDir|left`).
- `drink_image_map.json` — 음료 이미지 URL. 테이블 페이지(별도 wedding-table 사이트로 이전됨)용으로 남아 있음.
- `cloudinary.config.js` — 이미지 업로드 위젯 설정 (unsigned preset).
- `firebase.config.js` — 저장소에 없음. 없으면 JSON 맵 방식으로 동작.

## 동작
- `?admin=1`을 붙이면 관리자 모드 (옵션 이미지 업로드/교체). 기본은 고객 모드.
- 이미지 출처 우선순위: Firebase Realtime DB → `admin_option_image_map.json`.
- UI는 한국어/영어 전환 (`state.uiLang`). 문구를 추가하면 두 언어 모두 넣기.
- `pdf print` 버튼은 `#pdfSheet`를 인쇄 스타일로 출력.

## 작업 방식
- 로컬 확인: `python3 -m http.server`로 띄우고 Playwright로 고객 모드와 `?admin=1` 화면 스크린샷 확인.
- UI 스타일은 기존처럼 소문자 위주의 미니멀한 톤 유지.
- 단계를 추가하거나 삭제할 때는 `steps`, 렌더링 분기, PDF 요약(`buildSelectionRowsForPdf`)을 함께 수정.
