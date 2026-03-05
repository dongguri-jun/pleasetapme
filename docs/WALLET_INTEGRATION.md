# 지갑 개발자를 위한 연동 가이드

PleaseTapMe에 지갑 전용 버튼을 추가하려면, 앱에서 커스텀 URL 스킴을 지원해야 합니다.

## 필요한 작업

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

## 연동 요청

스킴이 준비되면 [Issue](https://github.com/dongguri-jun/pleasetapme/issues)를 열어주세요. 전용 버튼을 추가해드립니다.

필요한 정보:
- 지갑 이름
- URL 스킴 (예: `yourwallet:`)
- 앱스토어 링크 (iOS / Android)
- 지갑 로고 (선택)
