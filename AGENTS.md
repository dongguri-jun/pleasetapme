# PleaseTapMe - Agent Guide

## 프로젝트 컨텍스트
NFC Lightning 결제 수신 키링의 웹 런처. 단일 HTML 파일 정적 사이트.

## 에이전트별 가이드

### executor / deep-executor
- `index.html` 수정 시 CSS/JS/HTML 모두 인라인임을 인지
- JS 로직 변경 시 3개 뷰(랜딩, 셋업, 결제) 모두 영향 확인
- 지갑 URI 스킴 변경 시 iOS/Android 양쪽 테스트 필요
- QR 라이브러리(minified)는 절대 수정하지 말 것

### designer
- 디자인 변경 시 `docs/DESIGN_GUIDE.md` 반드시 참조
- 60-30-10 컬러 규칙 준수: Sky Blue / White / Mario Red
- Press Start 2P (헤드라인) + Inter (본문) 폰트 체계 유지
- 다크모드 `@media (prefers-color-scheme: dark)` 동시 업데이트 필수
- 게임 버튼 스타일 (box-shadow 3D push effect) 유지

### test-engineer / qa-tester
- 테스트 서버: `python3 -m http.server 8080`
- 필수 테스트 매트릭스:
  - 3개 뷰 전환 (hash routing)
  - 지갑 버튼 4개 (WoS, Phoenix, Blink, Zeus)
  - QR 코드 생성
  - 주소 복사 (clipboard API + fallback)
  - 셋업: 주소 입력 → URL 생성 → 복사 → Test
  - 라이트/다크 모드
  - iOS Safari + Android Chrome

### security-reviewer
- URL fragment(`#ln=`)는 서버로 전송 안 됨 (프라이버시 설계)
- 외부 리소스: Google Fonts CDN만 사용
- XSS 주의: `lnAddress`는 URL에서 추출, `textContent`로만 삽입 (innerHTML 지양)

### dependency-expert
- 외부 의존성 최소화 원칙
- 현재: Google Fonts (Press Start 2P, Inter), 인라인 QR 라이브러리
- 새 의존성 추가 시 반드시 인라인 가능 여부 확인

### writer
- 한국어 기본, 기술 용어는 영어 유지
- UI 텍스트는 간결하게 (결제 흐름에 방해 안 되게)
- NFC 가이드는 비기술 사용자 대상으로 작성
