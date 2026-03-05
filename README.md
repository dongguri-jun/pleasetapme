# PleaseTapMe

NFC 키링으로 Bitcoin Lightning 결제를 받을 수 있는 웹 런처.

**NFC 태그 → 웹페이지 → 지갑 실행 → 결제**

## 작동 방식

1. NFC 키링에 `https://pleasetap.me#ln=내주소@도메인` URL을 기록
2. 결제자가 키링을 스마트폰에 태그
3. 웹페이지가 열리고 Lightning 지갑이 실행됨
4. 금액 입력 후 결제 완료

## 특징

- 서버리스 — 정적 HTML 한 장, 백엔드 없음
- 프라이버시 — URL fragment(`#`)로 주소 전달, 서버에 노출 안 됨
- 지갑 독립 — 특정 지갑에 종속되지 않음
- iOS/Android 지원 — iOS NFC 제약을 웹 런처로 해결

## NFC 키링 설정

NFC 키링에 Lightning Address를 기록하는 방법은 [NFC 설정 가이드](docs/NFC_GUIDE.md)를 참고하세요.

## 지원 지갑

- [Wallet of Satoshi](https://www.walletofsatoshi.com/)
- [Phoenix](https://phoenix.acinq.co/)
- [Blink](https://www.blink.sv/)
- [Zeus](https://zeusln.com/)
- 기타 `lightning:` URI를 지원하는 모든 지갑

## 기술 스택

- HTML/CSS/JS (단일 파일, 프레임워크 없음)
- NFC: NTAG213
- Lightning: LUD-16 (Lightning Address)

## 라이선스

MIT
