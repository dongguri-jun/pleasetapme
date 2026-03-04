# PleaseTapMe - UI Design Guide

## 1. 디자인 컨셉

- **키워드**: Retro-Modern, Gamified, High-Energy, Simple
- **스타일**: 8비트/16비트 픽셀 아트 요소 + 현대적 플랫 UI
- **UX 원칙**: "태그하고 클릭하면 끝" — 최소 단계로 결제 유도

---

## 2. 컬러 팔레트 (60-30-10 Rule)

### Light Mode

| 역할 | 비율 | 색상명 | HEX | 적용 |
|------|------|--------|-----|------|
| 주조색 (Base) | 60% | Sky Blue | `#479FF8` | 배경, 메인 레이아웃 |
| 보조색 (Secondary) | 30% | Pure White | `#FFFFFF` | 카드, 텍스트 박스 |
| 강조색 (Accent) | 10% | Mario Red | `#E14D63` | CTA 버튼, 중요 강조 |

### 보조 컬러

| 이름 | HEX | 용도 |
|------|-----|------|
| Sky Dark | `#2D5A87` | 본문 텍스트, 라벨 |
| Sky Deeper | `#1e3f5e` | 깊은 강조 |
| Text Light | `#6a9fd8` | 보조 텍스트 |
| Red Dark | `#c13a4f` | 버튼 hover |
| Red Shadow | `#a02e3f` | 버튼 box-shadow (3D 효과) |

### Dark Mode

| 역할 | HEX | 적용 |
|------|-----|------|
| 배경 | `#1a2a3a` | body background |
| 카드 | `#1e2a36` | 카드 배경, border: rgba(255,255,255,0.08) |
| 텍스트 | `#e8eef4` | 기본 텍스트 |
| 보조 텍스트 | `#8ab4e0` | 라벨, 서브텍스트 |
| 입력 배경 | `rgba(0,0,0,0.3)` | input, result box |

---

## 3. 타이포그래피

| 용도 | 폰트 | 특징 |
|------|------|------|
| 헤드라인, 라벨, 브랜드 | `Press Start 2P` (Google Fonts) | 픽셀 폰트, 게임 느낌 |
| 본문, 데이터, 주소 | `Inter` (Google Fonts) | 가독성 높은 현대 산세리프 |
| Fallback | `-apple-system, BlinkMacSystemFont, sans-serif` | 시스템 폰트 |

### 폰트 크기 가이드

| 요소 | 폰트 | 크기 |
|------|------|------|
| 브랜드 타이틀 | Press Start 2P | 16px (카드 내) / 18px (랜딩) |
| 섹션 라벨 | Press Start 2P | 7-8px, uppercase, letter-spacing: 1px |
| 태그라인 | Press Start 2P | 11px |
| 본문 텍스트 | Inter | 13-14px |
| 주소 표시 | Inter (monospace) | 14px, font-weight: 600 |
| 버튼 텍스트 | Inter | 12-14px, font-weight: 700 |
| CTA 버튼 | Press Start 2P | 11px |

---

## 4. UI 컴포넌트

### 카드 (Card)

```css
background: #FFFFFF;           /* dark: #1e2a36 */
border-radius: 20px;
padding: 32px 24px;
box-shadow: 0 6px 0 rgba(0,0,0,0.1),
            0 12px 24px rgba(0,0,0,0.12);
```

### 게임 버튼 (3D Push Effect)

모든 버튼은 `box-shadow`로 3D 깊이감을 표현하고, `:active`에서 눌림 효과를 준다.

```css
/* 기본 상태 */
box-shadow: 0 4px 0 [darker-color];
transition: transform 0.1s;

/* 눌림 */
:active {
  transform: translateY(3px);
  box-shadow: 0 1px 0 [darker-color];
}
```

### CTA 버튼 (Mario Red)

```css
font-family: 'Press Start 2P', monospace;
font-size: 11px;
color: #FFFFFF;
background: #E14D63;
border-radius: 14px;
padding: 18px 24px;
box-shadow: 0 5px 0 #a02e3f;
```

### 지갑 버튼

2x2 그리드, 각 지갑 브랜드 컬러:

| 지갑 | 배경 | Shadow |
|------|------|--------|
| Wallet of Satoshi | `#f7931a` | `#c87615` |
| Phoenix | `#8b5cf6` | `#6d3ad4` |
| Blink | `#3b82f6` | `#2563d4` |
| Zeus | `#eab308` | `#b88d06` |

각 버튼에 `::before`로 8px 반투명 흰색 도트 인디케이터.

### 입력 필드

```css
padding: 14px;
font-size: 14px;
background: #f8fbff;          /* dark: rgba(0,0,0,0.3) */
border: 2px solid #d0e2f5;    /* dark: rgba(255,255,255,0.12) */
border-radius: 12px;
/* focus */
border-color: #479FF8;
```

### 결과/주소 박스

```css
background: #f0f6ff;
border: 2px dashed #b8d4f0;
border-radius: 12px;
font-family: 'Inter', monospace;
font-weight: 600;
color: #2D5A87;
```

### 스텝 번호 뱃지

```css
width: 22px; height: 22px;
font-family: 'Press Start 2P';
font-size: 8px;
color: #FFFFFF;
background: #479FF8;
border-radius: 6px;
```

---

## 5. 애니메이션

| 효과 | 적용 대상 | CSS |
|------|----------|-----|
| Pop In | 페이지 진입 | `scale(0.95) → scale(1)`, 0.35s cubic-bezier |
| Bounce | 번개 아이콘 | `translateY(0) → translateY(-6px)`, 2s infinite |
| Push Down | 모든 버튼 | `translateY(3-4px)` on `:active` |

---

## 6. 배경 효과

도트 패턴 (레트로 느낌):
```css
body::before {
  background-image: radial-gradient(rgba(255,255,255,0.08) 1px, transparent 1px);
  background-size: 16px 16px;
}
```

Dark mode: `rgba(255,255,255,0.03)`으로 더 은은하게.

---

## 7. 레이아웃

- **Max-width**: 400px (모바일 최적화)
- **Padding**: 20px (body), 32px 24px (카드)
- **Border-radius**: 20px (카드), 12-14px (버튼/입력), 6px (뱃지)
- **Gap**: 8px (그리드, 버튼 그룹)

---

## 8. 브랜드 마크

```
⚡ PleaseTapMe
```

- `Please` + `Me`: 기본 텍스트 색상
- `Tap`: Mario Red (`#E14D63`)
- 번개 이모지: bounce 애니메이션, `drop-shadow(0 3px 0 rgba(0,0,0,0.15))`

---

## 9. 페이지별 구성

### 랜딩 (카드 없음, 배경 위 직접)
- 큰 번개 아이콘 (52px)
- 브랜드 타이틀 (18px, 흰색 + text-shadow)
- 태그라인 (픽셀 폰트, 반투명 흰색)
- 설명 텍스트 (흰색)
- Red CTA 버튼: `TAP TO SETUP ⚡`
- 하단 안내 (반투명 흰색)

### 결제 (White 카드)
- Setup 링크 (pill 버튼, 상단)
- 브랜드 + 태그라인
- Lightning Address (dashed 박스)
- `SELECT WALLET` 라벨 (픽셀 폰트)
- 2x2 지갑 그리드
- Divider: `or scan` (픽셀 폰트)
- QR 코드
- Copy Address 버튼

### 셋업 (White 카드)
- ← Home 링크
- 브랜드
- 타이틀: `NFC KEYRING SETUP` (픽셀 폰트)
- 설명 텍스트
- Lightning Address 입력
- 생성된 URL 결과 박스 (dashed)
- Copy + Test 버튼
- 스텝 가이드 카드 (번호 뱃지)
