---
id: PTM-2
title: 웹 런처 페이지 구현
status: To Do
assignee: []
created_date: '2026-03-04 12:51'
updated_date: '2026-03-04 12:51'
labels: []
dependencies:
  - PTM-1
priority: high
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
NFC 태깅 후 열리는 정적 HTML 페이지 구현. URL fragment(#ln=...)에서 Lightning Address를 추출하고, OS를 감지하여 Android는 자동 리디렉트, iOS는 Pay 버튼을 표시한다. 폴백으로 QR 코드와 주소 복사 버튼 제공.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 - [ ] URL fragment에서 Lightning Address 파싱
- [ ] #2 OS 감지 (Android/iOS/기타)
- [ ] #3 Android: 자동 lightning: URI 리디렉트
- [ ] #4 iOS: Pay 버튼 클릭 시 lightning: URI 실행
- [ ] #5 QR 코드 생성 (폴백)
- [ ] #6 주소 복사 버튼 (폴백)
- [ ] #7 모바일 반응형 UI
- [ ] #8 단일 index.html 파일 (인라인 CSS/JS)
<!-- AC:END -->
