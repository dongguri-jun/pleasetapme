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

## 지원 지갑

- [Wallet of Satoshi](https://www.walletofsatoshi.com/)
- [Phoenix](https://phoenix.acinq.co/)
- [Blink](https://www.blink.sv/)
- [Zeus](https://zeusln.com/)
- 기타 `lightning:` URI를 지원하는 모든 지갑

지갑 개발자라면 [연동 가이드](docs/WALLET_INTEGRATION.md)를 참고하세요.

---

## NFC 키링 설정 가이드

### 준비물

- NFC 키링 (NTAG213 칩)
- 스마트폰 (NFC 지원)
- **NFC Tools** 앱 ([Android](https://play.google.com/store/apps/details?id=com.wakdev.wdnfc) / [iOS](https://apps.apple.com/app/nfc-tools/id1252962749))
- 자신의 Lightning Address (예: `myname@walletofsatoshi.com`)

> Lightning Address가 없다면? [Wallet of Satoshi](https://www.walletofsatoshi.com/), [Phoenix](https://phoenix.acinq.co/), [Blink](https://www.blink.sv/) 등의 지갑 앱에서 무료로 만들 수 있습니다.

### 1단계: 기록할 URL 준비

아래 형식으로 URL을 만드세요. `내주소@도메인` 부분을 자신의 Lightning Address로 바꿔주세요.

```
https://dongguri-jun.github.io/pleasetapme/#ln=내주소@도메인
```

**예시:**
```
https://dongguri-jun.github.io/pleasetapme/#ln=dongguri@walletofsatoshi.com
```

> 또는 웹사이트의 [Setup 페이지](https://dongguri-jun.github.io/pleasetapme/#setup)에서 자동으로 URL을 생성할 수 있습니다.

### 2단계: NFC 키링에 기록하기

**Android**

1. **NFC Tools** 앱을 열고 **Write** 탭을 선택
2. **Add a record** → **URL / URI** 선택
3. 1단계에서 만든 URL을 붙여넣기
4. **OK** → **Write** → NFC 키링을 스마트폰 뒷면에 대기
5. **"Write complete"** 메시지가 나오면 성공!

**iOS**

1. **NFC Tools** 앱을 열고 **Write** 탭을 선택
2. **Add a record** → **URL / URI** 선택
3. 1단계에서 만든 URL을 붙여넣기
4. **OK** → **Write** → NFC 키링을 iPhone 상단에 대기
5. **"Write complete"** 메시지가 나오면 성공!

> iPhone의 NFC 안테나는 상단(카메라 근처)에 있습니다.

### 3단계: 테스트하기

기록이 완료되면 반드시 테스트하세요!

- **Android**: 키링을 스마트폰 뒷면에 대기 → 브라우저 → 지갑 실행 확인
- **iOS**: 키링을 iPhone 상단에 대기 → 알림 탭 → Safari → 지갑 버튼 클릭

### 4단계: 하드웨어 락 (선택, 권장)

테스트 완료 후 NFC 태그를 **쓰기 방지** 설정하는 것을 권장합니다.

1. NFC Tools 앱에서 **Other** → **Lock Tag** 선택
2. NFC 키링을 대면 완료

> **주의: 하드웨어 락은 되돌릴 수 없습니다.** 한번 락을 걸면 영구적으로 내용을 변경할 수 없습니다. 반드시 테스트를 완료한 후에 락을 거세요.

### 문제 해결

| 증상 | 해결 |
|------|------|
| NFC 기록이 안 됨 | NFC 기능 켜져 있는지 확인. 키링을 더 가까이 대기 |
| 태깅은 되는데 지갑이 안 열림 | Lightning 지갑 앱 설치 확인. QR 코드 스캔 또는 주소 복사로 시도 |
| URL을 잘못 기록함 | 락 전이면 다시 기록. 락 후면 새 태그 사용 |

---

## 기술 스택

- HTML/CSS/JS (단일 파일, 프레임워크 없음)
- NFC: NTAG213
- Lightning: LUD-16 (Lightning Address)

## 라이선스

MIT
