# 타로카드 서비스 디자인 가이드 (DESIGN.md)
> **Midnight Mystique Gallery** — 심야의 어두운 미술관 한가운데 핀 조명을 받는 정교한 예술품처럼, 순수 흑색 캔버스 위에 신비로운 타로 카드 한 장을 무대 중심에 배치하고, 절제된 타이포그래피와 Apple Blue 컨트롤로 품격 있는 맞춤형 운세 경험을 제공합니다.

**Theme:** Dark (Midnight Museum)  
**Target Viewport:** Mobile Web First (최대 가로폭 430px 중앙 정렬 — iPhone Pro 기준)  
**기반 기술:** Next.js (App Router), Tailwind CSS v4, shadcn/ui

---

## 1. 디자인 철학 및 서비스 컨셉

### 1.1 컨셉: 정제된 심야의 타로 갤러리 (Midnight Gallery)
- **전시 공간으로서의 화면**: 번잡한 배너와 알록달록한 그라데이션을 배제하고, 완전한 흑색(Obsidian `#000000`) 캔버스 위에 하나의 타로 카드만을 집중 조명합니다.
- **광택과 1px의 정밀함 (Hairline Chrome)**: 부자연스러운 그림자 대신 1px의 섬세한 스틸 키라인(`--color-steel`, `#333336`)과 미세한 표면 명도 차이(Carbon `#1d1d1f`)로 카드와 컨트롤의 깊이감을 표현합니다.
- **절제된 액센트 (Apple Blue & Optical Gold)**: 전체 인터페이스는 모노크롬(흑/백/회색조)을 유지하되, 핵심 동작([타로 시작], [카드 한 장 뽑기], [이미지 저장])에만 **Apple Blue (`#0071e3`)**를 집중 배치하고, 타로 카드 번호와 별자리 심볼에만 **Optical Gold (`#ffd500`)**를 제한적으로 사용하여 신비감을 극대화합니다.
- **신뢰와 투명성 (Privacy-First UI)**: 개인정보를 저장하지 않고 즉시 폐기한다는 원칙(PRD 원칙 1)을 사용자가 직관적으로 체감할 수 있도록, 🔒 아이콘과 차분한 Ash(`#86868b`) 캡션으로 입력폼과 결과 카드 하단에 명확히 표기합니다.

### 1.2 화면별 공간 정의 (TARO_01~04 매핑)
1. **S-01 시작 화면 (F-1)**:
   - 미니멀한 흑색 스테이지에 신비로운 타로 카드 뒷면(Card Back) 배치
   - SF Pro Display 헤드라인과 차분한 소개 텍스트
   - 하단 170px 라디우스의 [타로 시작] Apple Blue 풀 필(Filled) 버튼
2. **S-02 내 정보 & 주제 선택 화면 (F-2)**:
   - 980px 라디우스의 정돈된 알약형 인풋 (이름, 생년월일, 선택 전공)
   - 6개 주제 (커리어, 재물, 연애, 건강, 학업, 종합) 2×3 그리드 토글 칩
   - 락(Lock) 아이콘 기반의 개인정보 즉시 파기 안내 카드
   - 필수 정보(이름, 생년월일, 주제) 완료 시 활성화되는 [카드 한 장 뽑기] 버튼
3. **S-03 맞춤 해석 결과 화면 (F-3~F-7)**:
   - 1초 이내 3D 카드 뒤집기 인터랙션
   - 1080×1350 (4:5 비율) 규격의 고해상도 독립 카드 캔버스 영역
   - 카드 일러스트레이션, 로마자 번호, 별자리 심볼(Optical Gold)
   - 3줄(90자 이내) 맞춤 해석문 (카드×주제 / 별자리 / 전공)
   - 액션 클러스터: [이미지 저장] (Apple Blue Filled), [결과 공유] (Electric Link Outlined)
   - 보조 액션: [다시 뽑기] (Ghost), [처음으로] (Subtle Charcoal)

---

## 2. 디자인 토큰 (Design Tokens)

### 2.1 색상 (Color Palette)

| 토큰명 | Hex / CSS Value | Tailwind Token | 역할 및 적용처 |
|---|---|---|---|
| **Obsidian** | `#000000` | `--color-obsidian` | 최상위 캔버스 배경, 풀블리드 스테이지, 카드 백그라운드 기본 |
| **Graphite** | `#0e0e0e` | `--color-graphite` | 플로팅 토스트/알림 배경, 네비게이션 헤더, 컨트롤 베이스 |
| **Carbon** | `#1d1d1f` | `--color-carbon` | 타로 카드 본체 배경, 폼 컨테이너, 모달/드로어 표면 |
| **Steel** | `#333336` | `--color-steel` | 1px 키라인 보더, 비활성 버튼 외곽선, 입력필드 기본 테두리 |
| **Slate** | `#6e6e73` | `--color-slate` | 입력필드 포커스 전 테두리, 보조 구분선, 서브 인터페이스 텍스트 |
| **Ash** | `#86868b` | `--color-ash` | 개인정보 안내문, 오락용 안내, 라벨 설명, 비활성 텍스트 |
| **Porcelain** | `#f5f5f7` | `--color-porcelain` | 어두운 표면 위의 기본 텍스트, 카드 3줄 해석 본문 |
| **White** | `#ffffff` | `--color-white` | 카드 명칭, 대형 헤드라인, 고대비 텍스트, 버튼 내 화이트 텍스트 |
| **Apple Blue** | `#0071e3` | `--color-apple-blue` | 핵심 CTA 버튼 ([타로 시작], [카드 뽑기], [이미지 저장]) |
| **Electric Link** | `#2997ff` | `--color-electric-link` | [결과 공유] 테두리/텍스트, 인라인 링크, 포커스 링 |
| **Optical Gold** | `#ffd500` | `--color-optical-gold` | 타로 카드 로마 숫자(XIX), 별자리 심볼(♌), 카드 프레임 하이라이트 |
| **Copper Status**| `#b64400` | `--color-copper-status` | 날짜 오류 메시지, 검증 경고 텍스트 (배지 형태 사용 금지) |

### 2.2 타이포그래피 (Typography)

- **주요 폰트**: `'SF Pro Text'`, `'SF Pro Display'`, Pretendard, Inter, system-ui, sans-serif
- **폰트 역할 분담**:
  - `SF Pro Display`: 카드 타이틀, 대형 헤드라인, 숫자/기호 표기
  - `SF Pro Text`: 입력 레이블, 안내 문구, 버튼 텍스트, 맞춤 해석 3줄 본문

#### Type Scale 명세

| 역할 | 패밀리 | 두께 | 크기 | 행간(Line-Height) | 자간(Tracking) | 용도 |
|---|---|---|---|---|---|---|
| `caption` | SF Pro Text | 400 | 12px | 1.33 | -0.12px | 오락용 안내, 개인정보 안내, 필드 캡션 |
| `caption-bold` | SF Pro Text | 600 | 12px | 1.33 | -0.12px | New 상태 표기, 강조 캡션 |
| `body` | SF Pro Text | 400 | 14px | 1.40 | -0.224px | 해석 3줄 본문, 보조 문구 |
| `body-strong` | SF Pro Text | 600 | 14px | 1.40 | -0.224px | 강조 텍스트, 입력 필드 인풋 텍스트 |
| `button` | SF Pro Text | 500 | 15px | 1.30 | -0.20px | 주요 버튼 텍스트 |
| `subtitle` | SF Pro Text | 500 | 17px | 1.47 | -0.374px | 서브 헤더, 섹션 제목 |
| `card-name` | SF Pro Display | 600 | 19px | 1.21 | 0.228px | 타로 카드 명칭 (XIX 태양) |
| `title-lg` | SF Pro Display | 600 | 28px | 1.15 | 0.196px | 메인 타이틀, 결과 헤더 |
| `display` | SF Pro Display | 600 | 36px | 1.10 | -0.50px | 시작 화면 메인 비주얼 슬로건 |

### 2.3 간격 & 레이아웃 (Spacing & Layout)

- **Mobile Viewport**: `max-w-[430px] mx-auto min-h-screen px-5 py-6`
- **Section Spacing**: 섹션 간 여백 `24px` (`--spacing-24`)
- **Component Gap**: 컴포넌트 간 여백 `12px` ~ `16px`
- **Padding**:
  - 카드 패널 내부 여백: `20px` ~ `24px`
  - 알약 버튼 패딩: 수직 `14px`, 수평 `24px` (컴팩트: `8px` × `16px`)
  - 폼 인풋 패딩: 수직 `14px`, 수평 `20px`

### 2.4 모서리 곡률 (Border Radius)

| 요소 | 라디우스 값 | CSS 토큰 | 비고 |
|---|---|---|---|
| **타로 카드 본체** | `28px` | `--radius-card` | 1080×1350 카드 캔버스 및 결과 프레임 |
| **폼 패널 / 컨테이너** | `24px` | `--radius-container`| 입력 폼 감싸는 Carbon 영역 |
| **버튼 (Buttons)** | `170px` (Full Pill) | `--radius-button` | Apple 스타일 알약 버튼 |
| **입력 인풋 (Inputs)** | `980px` (Full Pill) | `--radius-input` | 매끄러운 캡슐형 입력창 |
| **주제 칩 (Chips)** | `9999px` | `--radius-pill` | 토글 가능한 알약형 칩 |
| **다이얼로그 / 토스트**| `20px` | `--radius-modal` | 알림 및 팝업 모서리 |

### 2.5 깊이감 (Elevation & Keyline)
- 그림자(`box-shadow`) 효과를 원칙적으로 사용하지 않습니다.
- **Keyline 규격**:
  - `Subtle`: `1px solid rgba(255, 255, 255, 0.08)` (또는 `#333336`)
  - `Active/Focus`: `1px solid #0071e3` (포커스 링 오프셋 2px)
  - `Accent Border`: `1px solid rgba(255, 213, 0, 0.25)` (카드 골드 테두리 디테일)

---

## 3. Tailwind CSS v4 & shadcn/ui 설정

### 3.1 Tailwind CSS v4 `@theme` 정의

```css
@theme {
  /* Colors */
  --color-obsidian: #000000;
  --color-graphite: #0e0e0e;
  --color-carbon: #1d1d1f;
  --color-steel: #333336;
  --color-slate: #6e6e73;
  --color-ash: #86868b;
  --color-porcelain: #f5f5f7;
  --color-white: #ffffff;
  --color-apple-blue: #0071e3;
  --color-apple-blue-hover: #0077ed;
  --color-electric-link: #2997ff;
  --color-optical-gold: #ffd500;
  --color-copper-status: #b64400;

  /* Typography */
  --font-sans: 'SF Pro Text', -apple-system, BlinkMacSystemFont, 'Pretendard', sans-serif;
  --font-display: 'SF Pro Display', -apple-system, BlinkMacSystemFont, 'Pretendard', sans-serif;

  /* Border Radii */
  --radius-card: 28px;
  --radius-container: 24px;
  --radius-button: 170px;
  --radius-input: 980px;
  --radius-pill: 9999px;
  --radius-modal: 20px;

  /* Custom Transitions & Keyframes */
  --animate-flip: card-flip 0.8s cubic-bezier(0.34, 1.56, 0.64, 1) forwards;
}

@keyframes card-flip {
  0% {
    transform: rotateY(180deg) scale(0.95);
  }
  100% {
    transform: rotateY(0deg) scale(1);
  }
}
```

### 3.2 shadcn/ui CSS 변수 매핑 (`globals.css`)

```css
@layer base {
  :root,
  .dark {
    --background: #000000;          /* Obsidian */
    --foreground: #f5f5f7;          /* Porcelain */

    --card: #1d1d1f;                /* Carbon */
    --card-foreground: #f5f5f7;

    --popover: #0e0e0e;             /* Graphite */
    --popover-foreground: #f5f5f7;

    --primary: #0071e3;             /* Apple Blue */
    --primary-foreground: #ffffff;

    --secondary: #1d1d1f;           /* Carbon */
    --secondary-foreground: #f5f5f7;

    --muted: #0e0e0e;               /* Graphite */
    --muted-foreground: #86868b;     /* Ash */

    --accent: #333336;              /* Steel */
    --accent-foreground: #ffffff;

    --destructive: #b64400;         /* Copper Status */
    --destructive-foreground: #ffffff;

    --border: #333336;              /* Steel */
    --input: #333336;               /* Steel Hairline */
    --ring: #0071e3;                /* Apple Blue */

    --radius: 1.75rem;              /* 28px */
  }

  body {
    background-color: var(--background);
    color: var(--foreground);
    font-family: var(--font-sans);
    -webkit-font-smoothing: antialiased;
    letter-spacing: -0.015em;
  }
}
```

---

## 4. 컴포넌트별 상세 규칙 (Component Rules)

### 4.1 타로 카드 컴포넌트 (`TarotCard`)
- **규격 및 비율**: 
  - 세로형 비율 4:5 (모바일 뷰: 너비 `100%`, 최대 `360px`, 높이 `450px`)
  - 내보내기 캔버스: `1080px × 1350px`
- **모서리**: `28px` (`rounded-[28px]`), 오버플로우 숨김(`overflow-hidden`)
- **표면 및 테두리**: 
  - 배경: Obsidian `#000000` 위에 Carbon `#1d1d1f` 그라데이션
  - 테두리: `1px solid rgba(255, 255, 255, 0.1)` + 카드 테두리 내부 `1px solid rgba(255, 213, 0, 0.15)`
- **3D 뒤집기 효과**:
  - `perspective: 1000px`, `transform-style: preserve-3d`
  - 1초 이내(0.8s) 정밀 뒤집기 인터랙션
- **카드 내부 정보 계층 (상단 → 하단)**:
  1. **헤더 라벨**: `{이름}님의 타로 · {주제}` (14px, Ash `#86868b`)
  2. **카드 아트워크**: 고해상도 아르카나 일러스트 (중앙 배치, 20px 곡률)
  3. **카드 명칭 & 별자리**: `XIX 태양 · ♌ 사자자리` (18px SF Pro Display, Optical Gold `#ffd500`)
  4. **맞춤 3줄 해석 (90자 이내)**:
     - 1줄: 카드 × 주제 기본 문장
     - 2줄: 별자리 문장
     - 3줄: 전공 계열 문장 (미입력 시 미출력)
     - 폰트: 14px Porcelain `#f5f5f7`, 줄간격 1.5, 줄바꿈 자연스럽게
  5. **워터마크/안내**: `※ 오락용 타로 해석입니다` (12px, Ash `#86868b`)

### 4.2 버튼 컴포넌트 (`Button` — shadcn Variant)

| Variant | 외관 스타일 | 용도 및 화면 매핑 |
|---|---|---|
| **Default (Primary)** | Background `#0071e3`, Text `#ffffff`, Hover `#0077ed`, Rounding `170px` (Pill), 높이 `50px` | [타로 시작] (S-01), [카드 한 장 뽑기] (S-02), [이미지 저장] (S-03) |
| **Secondary (Outline)**| Background `transparent`, Border `1px solid #2997ff`, Text `#2997ff`, Rounding `170px` | [결과 공유] (S-03) |
| **Muted/Subtle** | Background `#1d1d1f`, Border `1px solid #333336`, Text `#f5f5f7`, Rounding `170px` | [다시 뽑기] (S-03) |
| **Ghost** | Background `transparent`, Text `#86868b`, Hover Text `#ffffff` | [처음으로] (S-03), 뒤로가기 |
| **Disabled** | Background `#333336`, Text `#6e6e73`, Cursor `not-allowed`, 테두리 없음 | 필수 입력값 누락 시의 [카드 뽑기] 버튼 |

### 4.3 폼 인풋 컴포넌트 (`Input` & `Form`)
- **형태**: 알약형 캡슐 (`rounded-full`, 980px)
- **크기**: 높이 `48px`, 좌우 패딩 `20px`
- **배경 & 테두리**: 
  - 기본: Background `rgba(255, 255, 255, 0.04)`, Border `1px solid #333336`, Text `#f5f5f7`
  - 포커스: Border `1px solid #0071e3`, Ring `0 0 0 2px rgba(0, 113, 227, 0.3)`
  - 플레이스홀더: Text `#6e6e73`
- **오류 상태**: 
  - 생년월일 불일치 시: Border `1px solid #b64400`
  - 오류 문구: 12px `#b64400` ("날짜를 다시 확인해 주세요")

### 4.4 주제 선택 칩 (`TopicSelector`)
- **레이아웃**: 2행 3열 그리드 (`grid grid-cols-3 gap-2.5`)
- **형태**: 높이 `42px`, `rounded-full`, 중앙 정렬
- **상태 변화**:
  - **비선택**: Background `#1d1d1f`, Border `1px solid #333336`, Text `#86868b`
  - **선택됨**: Background `#0e0e0e`, Border `1.5px solid #0071e3`, Text `#ffffff`, Font-Weight 600

### 4.5 토스트 & 피드백 (`Sonner` / `Toast`)
- **형태**: 하단 플로팅 캡슐 (`rounded-[20px]`, `px-5 py-3.5`)
- **배경**: Graphite `#0e0e0e` (블러 12px) + 테두리 `1px solid #333336`
- **텍스트**: 13px Porcelain `#f5f5f7`
- **표시 케이스**:
  - "이미지를 저장했어요"
  - "이미지를 길게 눌러 저장해 주세요"
  - "결과를 복사했어요. 원하는 앱에 붙여 넣어 주세요"
  - "아래 글을 길게 눌러 복사해 주세요"

### 4.6 개인정보 즉시 파기 안내 패널 (`PrivacyNoticeBox`)
- **스타일**: Background `rgba(29, 29, 31, 0.5)`, `rounded-[20px]`, 테두리 `1px solid #333336`, `p-3.5`
- **내용**: 🔒 아이콘 + 12px Ash `#86868b` 텍스트
- **문구**: *"입력한 이름 · 생년월일 · 전공은 해석을 만드는 데만 쓰고, 서버로 보내거나 저장하지 않아요. 창을 닫거나 [처음으로]를 누르면 바로 지워져요."*

---

## 5. 원칙 및 Do's & Don'ts

### Do
- 캔버스는 순수 흑색 Obsidian(`#000000`)을 유지하여 카드와 컨트롤이 전시장 조명처럼 부각되도록 합니다.
- 타로 카드는 4:5 비율(1080×1350)과 28px 라디우스를 고수하여 인스타그램 스토리나 모바일 메신저에 최적화합니다.
- 중요한 전환 버튼에만 Apple Blue(`#0071e3`)를 사용하고, 텍스트 링크와 공유 테두리에는 Electric Link(`#2997ff`)를 사용합니다.
- 카드 명칭과 별자리 기호에만 Optical Gold(`#ffd500`)를 제한적으로 사용하여 모던한 신비감을 부여합니다.
- 개인정보는 서버로 전송되지 않음을 입력 화면과 결과 화면 하단에 차분하게 항시 명시합니다.

### Don't
- 화려한 보라색/그라데이션 네온 효과나 저품질 그림자(`box-shadow: 0 10px 30px rgba(...)`)를 남발하지 않습니다.
- 버튼 모서리를 직각이나 4px로 각지게 만들지 않고, 정제된 170px 알약형(Pill)을 준수합니다.
- Copper Status(`#b64400`) 색상을 에러 알림 외에 구매/시작 버튼에 사용하지 않습니다.
- 결과 카드 이미지나 공유 텍스트에 생년월일이나 전공 원문을 절대 노출하지 않습니다.
- 3줄 해석의 길이를 90자 이상으로 늘여 카드의 비주얼 여백을 해치지 않습니다.
