# NFC 키링 설정 가이드

PleaseTapMe NFC 키링에 자신의 Lightning Address를 기록하는 방법을 안내합니다.

## 준비물

- NFC 키링 (NTAG213 칩)
- 스마트폰 (NFC 지원)
- **NFC Tools** 앱 ([Android](https://play.google.com/store/apps/details?id=com.wakdev.wdnfc) / [iOS](https://apps.apple.com/app/nfc-tools/id1252962749))
- 자신의 Lightning Address (예: `myname@walletofsatoshi.com`)

> Lightning Address가 없다면? [Wallet of Satoshi](https://www.walletofsatoshi.com/), [Phoenix](https://phoenix.acinq.co/), [Blink](https://www.blink.sv/) 등의 지갑 앱에서 무료로 만들 수 있습니다.

---

## 1단계: 기록할 URL 준비

아래 형식으로 URL을 만드세요. `내주소@도메인` 부분을 자신의 Lightning Address로 바꿔주세요.

```
https://dongguri-jun.github.io/pleasetapme/#ln=내주소@도메인
```

**예시:**
```
https://dongguri-jun.github.io/pleasetapme/#ln=dongguri@walletofsatoshi.com
```

> 또는 웹사이트의 Setup 페이지에서 자동으로 URL을 생성할 수 있습니다:
> https://dongguri-jun.github.io/pleasetapme/#setup

---

## 2단계: NFC 키링에 기록하기

### Android

1. **NFC Tools** 앱을 열고 **Write** 탭을 선택
2. **Add a record** 누르기
3. **URL / URI** 선택
4. 1단계에서 만든 URL을 붙여넣기
5. **OK** → **Write** 누르기
6. NFC 키링을 스마트폰 뒷면에 가까이 대기
7. **"Write complete"** 메시지가 나오면 성공!

### iOS

1. **NFC Tools** 앱을 열고 **Write** 탭을 선택
2. **Add a record** 누르기
3. **URL / URI** 선택
4. 1단계에서 만든 URL을 붙여넣기
5. **OK** → **Write** 누르기
6. **"Ready to write"** 메시지가 나오면 NFC 키링을 iPhone 상단에 가까이 대기
7. **"Write complete"** 메시지가 나오면 성공!

> iPhone의 NFC 안테나는 상단(카메라 근처)에 있습니다. 키링을 iPhone 상단에 대세요.

---

## 3단계: 테스트하기

기록이 완료되면 반드시 테스트하세요!

### Android
1. NFC 키링을 스마트폰 뒷면에 가까이 대기
2. 브라우저가 열리면서 결제 페이지가 나타남
3. 지갑 버튼을 눌러 지갑 앱이 실행되는지 확인

### iOS
1. NFC 키링을 iPhone 상단에 가까이 대기
2. 알림이 뜨면 탭하여 Safari로 이동
3. 결제 페이지에서 지갑 버튼을 눌러 지갑 앱이 실행되는지 확인

> 테스트에서 자신의 주소가 올바르게 표시되고, 지갑이 정상적으로 열리면 성공입니다.

---

## 4단계: 하드웨어 락 (선택, 권장)

테스트가 완료되면 NFC 태그를 **쓰기 방지** 설정하는 것을 강력히 권장합니다.

### 왜 필요한가요?
- 다른 사람이 NFC 키링의 내용을 변경하는 것을 방지합니다
- 악의적인 사용자가 URL을 자신의 주소로 덮어쓸 수 있습니다

### 방법
1. NFC Tools 앱에서 **Other** 탭 선택
2. **Lock Tag** (또는 **Make Read Only**) 선택
3. NFC 키링을 대면 완료

### !! 주의사항 !!

- **하드웨어 락은 되돌릴 수 없습니다** (비가역적)
- 한번 락을 걸면 **영구적으로** 내용을 변경할 수 없습니다
- Lightning Address를 바꾸고 싶으면 새 NFC 태그를 사용해야 합니다
- **반드시 테스트를 완료한 후에** 락을 거세요
- 오타가 있으면 태그를 버려야 합니다

---

## 문제 해결

### NFC 기록이 안 돼요
- 스마트폰의 NFC 기능이 켜져 있는지 확인하세요
- Android: 설정 → 연결 → NFC 켜기
- iOS: 별도 설정 없음 (iPhone 7 이상 기본 지원)
- 키링을 스마트폰에 더 가까이 대보세요

### 태깅은 되는데 지갑이 안 열려요
- Lightning 지갑 앱이 설치되어 있는지 확인하세요
- 결제 페이지에서 QR 코드를 다른 지갑으로 스캔해보세요
- 주소 복사 버튼으로 직접 지갑에 붙여넣을 수도 있습니다

### URL을 잘못 기록했어요
- 하드웨어 락을 걸지 않았다면: NFC Tools로 다시 기록하면 됩니다
- 하드웨어 락을 걸었다면: 새 NFC 태그를 사용해야 합니다
