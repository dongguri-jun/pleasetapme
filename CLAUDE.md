# PleaseTapMe - Claude Code Project Guide

## 프로젝트 개요
NFC 키링을 통해 Lightning Network 결제를 받을 수 있는 웹 런처 서비스.
NFC 태그 → 웹페이지 → 지갑 실행 → 결제.

## 아키텍처
- **단일 파일**: `index.html` (인라인 CSS/JS, 외부 프레임워크 없음)
- **서버리스**: 정적 호스팅, 백엔드/DB 없음
- **프라이버시**: URL fragment(`#ln=`)로 주소 전달, 서버로 전송 안 됨

## 3개 뷰 (URL hash 기반)
1. **랜딩** (hash 없음) - 제품 소개 + Setup CTA
2. **셋업** (`#setup`) - Lightning Address 입력 → NFC URL 생성
3. **결제** (`#ln=address`) - 지갑 버튼 + QR 코드 + 주소 복사

## 핵심 기술
- **지갑별 URI 스킴**: `walletofsatoshi:`, `phoenix:`, `blink:`, `zeusln:`
- **iOS 제약**: `lightning:` NFC 미지원 → HTTPS 웹 런처 경유, 사용자 제스처 필수
- **Android**: 자동 리디렉트 가능
- **루프 방지**: `launching` 플래그 + 3초 쿨다운

## 디자인 시스템
- **컨셉**: Retro-Modern (마리오풍 픽셀 아트 + 현대 플랫 UI)
- **60-30-10**: Sky Blue `#479FF8` / White `#FFFFFF` / Mario Red `#E14D63`
- **폰트**: Press Start 2P (헤드라인) + Inter (본문)
- **다크모드**: `prefers-color-scheme: dark` CSS 미디어 쿼리
- **상세**: `docs/DESIGN_GUIDE.md` 참조

## 코딩 규칙
- 모든 코드는 `index.html` 단일 파일에 인라인
- vanilla JS만 사용 (프레임워크 금지)
- QR 코드 라이브러리는 인라인 minified 포함
- 외부 의존성: Google Fonts (Press Start 2P, Inter)만 허용
- 기존 JS 로직 수정 시 모든 뷰에서 테스트 필수

## 파일 구조
```
index.html              # 메인 (유일한) 제품 파일
docs/SPEC.md            # 제품 스펙
docs/DESIGN_GUIDE.md    # UI 디자인 가이드
backlog/                # 태스크 관리
```

## 테스트
- 로컬: `python3 -m http.server 8080`
- 모바일: Tailscale IP로 접속 (현재 100.88.49.37:8080)
- 필수 테스트 항목: 3개 뷰 전환, 지갑 버튼 4개, QR 생성, 주소 복사, 셋업 플로우
