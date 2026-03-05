---
id: PTM-7
title: QR 코드 생성 버그 수정
status: Done
assignee: []
created_date: '2026-03-05 02:16'
labels: []
dependencies: []
priority: high
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
인라인 QR 라이브러리 IIFE 버그로 QR 생성 실패. 라이브러리를 qrcode-generator@1.4.4 CDN으로 교체하고 createImgTag() API 사용.
<!-- SECTION:DESCRIPTION:END -->

## Final Summary

<!-- SECTION:FINAL_SUMMARY:BEGIN -->
깨진 인라인 라이브러리 제거, CDN qrcode-generator@1.4.4로 교체, 스캔 가능한 QR 확인됨.
<!-- SECTION:FINAL_SUMMARY:END -->
