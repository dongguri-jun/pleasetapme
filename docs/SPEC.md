# PleaseTapMe - Product Specification

## 1. 개요

### 제품 정의
NFC 키링을 통해 Lightning Network 결제를 받을 수 있는 개인 수신 태그 제품 + 웹 런처 서비스.

### 문제
- Bitcoin Lightning으로 결제를 받으려면 QR 코드를 보여주거나 주소를 직접 알려줘야 한다
- NFC에 `lightning:` URI를 직접 저장하면 iOS에서 작동하지 않는다
- 기존 Lightning NFC 제품(Bolt Card 등)은 "보내는" 용도이며, "받는" 용도 제품은 거의 없다

### 솔루션
NFC 키링에 `https://pleasetap.me` URL을 저장하고, 웹 런처 페이지가 OS를 감지하여 Lightning 지갑을 실행한다.

### 타겟 사용자
- Bitcoin Lightning 사용자 (개인 팁 수신)
- Bitcoin 커뮤니티 굿즈 구매자
- 소규모 상점 (Lightning 결제 수단)

### 성공 지표
- NFC 태깅 → 지갑 실행 성공률 (목표: Android 95%+, iOS 90%+)
- 평균 태깅 → 결제 완료 시간 (목표: 10초 이내)

---

## 2. 핵심 기능

### F1: NFC → 웹 런처 → 지갑 실행
사용자의 Lightning Address가 포함된 URL을 NFC 태그에서 읽고, 웹페이지를 통해 지갑 앱을 실행한다.

### F2: OS별 분기 처리
- **Android**: 자동으로 `lightning:` URI 실행 → 지갑 바로 열림
- **iOS**: "Pay" 버튼 표시 → 사용자 클릭 → 지갑 실행 (iOS 제약: 사용자 제스처 필수)

### F3: 폴백 UI
- 지갑이 없거나 실행 실패 시: QR 코드 표시 + 주소 복사 버튼

---

## 3. 시스템 아키텍처

### 전체 흐름

```
NFC 태그 (NTAG213)
  └─ https://pleasetap.me#ln=user@domain.com
        ↓
정적 웹페이지 (pleasetap.me)
  - URL fragment(#ln=...)에서 Lightning Address 추출
  - OS 감지 (Android/iOS)
  ┌─ Android → 자동 lightning: URI 실행
  └─ iOS → "Pay" 버튼 → 클릭 시 lightning: URI 실행
        ↓
사용자 Lightning 지갑 앱
  - 주소 자동 입력
  - 금액 입력
  - 전송
```

### 핵심 설계 원칙

1. **서버리스**: 정적 HTML 1장. 백엔드/DB/계정 시스템 없음
2. **프라이버시**: `#` 뒤의 fragment는 서버로 전송되지 않음. 주소는 NFC 태그 안에만 존재
3. **탈중앙**: 특정 지갑/서비스에 종속되지 않음

### 호스팅
- Cloudflare Pages / GitHub Pages / Vercel 중 택 1
- 도메인: `pleasetap.me`

---

## 4. 기술 스펙

### 4.1 NFC 태그

| 항목 | 값 |
|------|-----|
| 칩 | NTAG213 (권장) |
| 메모리 | 144 bytes (NDEF 137 bytes) |
| 저장 형식 | NDEF URI Record |
| 저장 값 | `https://pleasetap.me#ln=user@domain.com` |
| 예상 사용량 | ~49 bytes (여유 ~88 bytes) |
| 보안 | 기록 후 하드웨어 락 (OTP fuse, 비가역) |

### 4.2 URL 구조

```
https://pleasetap.me#ln=<lightning_address>
```

- `#ln=` 뒤에 Lightning Address를 그대로 넣는다
- 예: `https://pleasetap.me#ln=dongguri@oksu.su`
- fragment는 서버로 전송되지 않으므로 개인정보 보호

### 4.3 Lightning Address 표준 (LUD-16)

```
user@domain.com
  ↓ 지갑이 내부적으로 변환
GET https://domain.com/.well-known/lnurlp/user
  ↓ 서버 응답
{
  "tag": "payRequest",
  "callback": "https://domain.com/api/lnurl/callback/user",
  "minSendable": 1000,
  "maxSendable": 500000000
}
  ↓ 지갑이 invoice 요청 → 결제
```

### 4.4 OS별 동작 (검증 완료)

#### iOS
- NFC 백그라운드 태그 읽기: `http(s)://`, `tel:`, `sms:`, `mailto:` **만** 지원
- **`lightning:` 커스텀 스킴은 NFC에서 완전히 무시됨** (알림조차 없음)
- Safari에서 `window.location.href = "lightning:..."` → **사용자 제스처(버튼 클릭) 필수**
- 자동 리디렉트는 iOS 13부터 차단됨

#### Android
- NFC `ACTION_NDEF_DISCOVERED` intent로 커스텀 스킴 지원
- `lightning:` URI → 등록된 지갑 앱 실행 (또는 앱 선택 UI)
- 웹페이지에서 자동 리디렉트 허용

#### 지갑 선택
- 어떤 지갑이 열릴지는 **OS가 결정** (NFC/웹페이지에서 제어 불가)
- iOS: `lightning:` 스킴 등록된 앱 중 iOS 내부 규칙으로 선택 (undefined behavior)
- Android: 사용자에게 앱 선택 UI 표시 가능

### 4.5 웹페이지 기술 요구사항

| 항목 | 값 |
|------|-----|
| 파일 | `index.html` (단일 파일, 인라인 CSS/JS) |
| 프레임워크 | 없음 (vanilla HTML/CSS/JS) |
| 외부 의존성 | QR 코드 라이브러리 1개 (인라인 또는 CDN) |
| 반응형 | 모바일 최적화 필수 |
| HTTPS | 필수 (NFC NDEF URI가 https 요구) |

---

## 5. UX 흐름

### 5.1 소비자 (NFC 키링 구매자) 설정 흐름

```
1. NFC 키링 수령
2. NFC Tools 앱 설치 (iOS/Android)
3. Write → URL/URI 선택
4. 입력: https://pleasetap.me#ln=자신의라이트닝주소
5. NFC 키링에 기록
6. 태깅 테스트
7. (선택) 하드웨어 락으로 쓰기 방지
```

### 5.2 결제자 (태깅하는 사람) 흐름

#### Android
```
NFC 키링 태깅
  → 브라우저 열림
  → 자동으로 Lightning 지갑 실행
  → 금액 입력
  → 전송
```

#### iOS
```
NFC 키링 태깅
  → Safari 열림
  → "Pay" 버튼 표시
  → 버튼 클릭
  → Lightning 지갑 실행
  → 금액 입력
  → 전송
```

#### 폴백 (지갑 미설치 등)
```
NFC 키링 태깅
  → 브라우저 열림
  → 지갑 실행 실패
  → QR 코드 표시 + 주소 복사 버튼
```

### 5.3 웹 런처 페이지 UI 요소

1. **Lightning Address 표시** (예: pleasetapme@oksu.su)
2. **"Pay" 버튼** (iOS 필수, Android에서도 폴백으로 표시)
3. **QR 코드** (lightning: URI 인코딩)
4. **주소 복사 버튼**
5. **브랜딩**: PleaseTapMe 로고 + ⚡

---

## 6. 제약사항 & 리스크

### 기술적 제약
| 제약 | 영향 | 대응 |
|------|------|------|
| iOS에서 `lightning:` NFC 미지원 | iPhone 사용자는 NFC → 직접 지갑 실행 불가 | HTTPS 웹 런처 페이지 경유 |
| iOS에서 자동 리디렉트 차단 | 버튼 클릭 1회 추가 필요 | "Pay" 버튼 UX 최적화 |
| 지갑 선택 불가 | 특정 지갑 강제 실행 불가능 | 수용 (업계 표준과 동일) |
| NFC 하드웨어 락 비가역 | 오타 시 태그 폐기 | 락 전 테스트 필수 안내 |

### 보안
| 위협 | 위험도 | 대응 |
|------|--------|------|
| 태그 복제 | 낮음 | 복제해도 공격자 이득 없음 (돈이 원래 주인에게 감) |
| 태그 덮어쓰기 | 중간 | 하드웨어 락으로 방지 (OTP fuse) |
| 중간자 공격 | 낮음 | HTTPS + Lightning 프로토콜 자체 보안 |

