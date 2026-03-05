---
id: PTM-4
title: 실제 NFC 태그 테스트
status: To Do
assignee: []
created_date: '2026-03-04 12:51'
updated_date: '2026-03-05 02:16'
labels: []
dependencies:
  - PTM-1
priority: high
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
NTAG213 태그에 pleasetap.me URL을 기록하고 iOS/Android에서 실제 동작 테스트. 다양한 지갑(WoS, Phoenix, Zeus 등)에서 결제 흐름 확인.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 - [ ] NTAG213에 테스트 URL 기록
- [ ] #2 Android 태깅 → 지갑 실행 확인
- [ ] #3 iOS 태깅 → Safari → Pay 버튼 → 지갑 실행 확인
- [ ] #4 지갑 미설치 시 QR/복사 폴백 확인
- [ ] #5 다양한 Lightning Address 도메인 테스트 (oksu.su, walletofsatoshi.com 등)
<!-- AC:END -->
