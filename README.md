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

## 지갑 개발자를 위한 연동 가이드

PleaseTapMe에 지갑 전용 버튼을 추가하려면, 앱에서 커스텀 URL 스킴을 지원해야 합니다.

### 필요한 작업

**1. 커스텀 URL 스킴 등록**

Android (`AndroidManifest.xml`):
```xml
<activity android:name=".MainActivity">
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        <data android:scheme="yourwallet" />
    </intent-filter>
</activity>
```

iOS (`Info.plist`):
```xml
<key>CFBundleURLTypes</key>
<array>
    <dict>
        <key>CFBundleURLSchemes</key>
        <array>
            <string>yourwallet</string>
        </array>
    </dict>
</array>
```

**2. `lightning:` 범용 스킴 지원 (권장)**

위와 동일한 방법으로 `lightning` 스킴도 등록하면, PleaseTapMe뿐 아니라 모든 Lightning 서비스에서 지갑이 호출됩니다.

**3. URI 처리**

앱이 `yourwallet:user@domain.com` 형태의 URI를 받으면, Lightning Address로 인식하여 결제 화면을 열어야 합니다.

### 연동 요청

스킴이 준비되면 [Issue](https://github.com/dongguri-jun/pleasetapme/issues)를 열어주세요. 전용 버튼을 추가해드립니다.

필요한 정보:
- 지갑 이름
- URL 스킴 (예: `yourwallet:`)
- 앱스토어 링크 (iOS / Android)
- 지갑 로고 (선택)

## 기술 스택

- HTML/CSS/JS (단일 파일, 프레임워크 없음)
- NFC: NTAG213
- Lightning: LUD-16 (Lightning Address)

## 라이선스

MIT
