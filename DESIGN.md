# 오늘의 타로 디자인 가이드 (DESIGN.md)

> 연회색 배경 위의 흰 라운드 카드, 선명한 초록 포인트, 읽기 쉬운 한글 타이포그래피로 만드는 가벼운 맞춤형 타로 경험.

## 0. 기준과 적용 범위

- **디자인 원본:** [명지대학교 타로 디자인 팩 · Figma](https://www.figma.com/design/ByJWTlSJ9Oj0nJMj9Ie72E/?node-id=4-13)
  - 디자인 가이드: `4:13`, 컴포넌트: `3:25`, 화면 예시: `5:134`.
- **제품 기준:** [PRD](TARO_01_PRD.md), [기능명세서](TARO_02_기능명세서.md), [유저플로우](TARO_03_유저플로우.md), [와이어프레임](TARO_04_와이어프레임.md).
- **원본 확인값:** Figma 변수·텍스트 스타일·컴포넌트 속성과 화면에서 직접 확인한 값이다. 간격·크기·곡률은 별도 변수로 등록되어 있지 않아 실측값을 기록했다.
- **승인된 보완:** 사용자가 선택한 ① 접근성 우선 구현, ② 1080×1350 전용 저장 레이아웃과 하단 서비스 이름 추가. 원본 토큰은 보존하고 구현용 의미 토큰을 분리한다. 아래의 구체적인 보완 수치는 이 방향에 따른 구현 기준이며 Figma에 이미 존재하는 값이 아니다.
- **구현 보완:** 원본에 없는 반응형·키보드·진행 중 상태 등은 이 문서에서 추가한 기준으로 명시한다.
- 우선순위: **개인정보·제품 요구사항 → 승인된 접근성/저장 보완 → Figma 원본 → 기타 구현 보완**.
- 이 문서는 기존 검정 배경·파랑 CTA·금색 강조·SF Pro·알약형 버튼 규칙을 대체한다. 별도 다크 테마는 정의하지 않는다.
- 기존 가이드의 기술 전제인 Next.js App Router / Tailwind CSS v4 / shadcn/ui는 유지한다. 현재 저장소에는 문서만 있으므로 실제 앱 구현·빌드가 존재하거나 검증되었다는 뜻은 아니다.

## 1. 디자인 방향

- `color/bg` 연회색 캔버스에 `color/surface` 흰 카드와 입력 필드를 배치한다.
- 초록은 주요 행동·선택·카드 메타 정보에 제한한다. 스와이프 일러스트용 초록과 UI 강조색을 구분한다.
- 화면당 주요 행동은 하나. **결과 화면에서는 [결과 공유]만 Primary**, 이미지 저장·다시 뽑기·처음으로는 Secondary다.
- 개인정보 안내를 입력 필드 바로 아래와 결과 화면에 노출한다. 이름은 저장 이미지·공유에 포함되므로 닉네임을 권장한다.
- 건강·재물 해석은 예언이나 단정이 아니라 돌아볼 관점으로 쓴다. 결과·저장 이미지·공유 메시지에 오락용 안내를 넣는다.
- 레퍼런스 uibowl 화면은 연회색/흰 카드/초록 구조만 참고했다. 해당 레퍼런스의 캐릭터·브랜드·카드 그림을 재사용하지 않는다.

## 2. 색상

### 2.1 Figma 원본 토큰

컬렉션 `Taro`의 변수명은 아래와 같다. 단일 모드에서 확인했으며 다크 모드는 확인되지 않았다.

| 변수 | 원본 HEX | 역할 |
|---|---|---|
| `color/bg` | `#F3F3F5` | 페이지 배경 |
| `color/surface` | `#FFFFFF` | 카드·입력·Secondary 버튼 |
| `color/surface-sub` | `#F6F6F8` | 개인정보 안내 등 보조 표면 |
| `color/text/primary` | `#000000` | 제목·본문·입력값 |
| `color/text/secondary` | `#4D4D4E` | 보조 설명·입력 라벨 |
| `color/text/tertiary` | `#979F9B` | 원본 placeholder·오락용 안내 |
| `color/text/on-accent` | `#FFFFFF` | 원본 Primary/Disabled 글자·토스트 글자 |
| `color/border` | `#DCDCDD` | 원본 입력·버튼·칩 테두리 |
| `color/accent` | `#00D959` | 주요 행동 배경·선택 |
| `color/accent-soft` | `#E6FAEF` | 선택 칩·보조 강조 표면 |
| `color/accent-strong` | `#00D959` | 원본 카드 메타·선택 칩 글자; accent와 같은 값 |
| `color/disabled` | `#D7D7D7` | 비활성 버튼 배경 |
| `color/danger` | `#E5484D` | 원본 오류 테두리·문구 |
| `color/inverse` | `#232427` | 토스트 배경 |
| `color/accent-illust` | `#00DE00` | 스와이프 안내 일러스트 |

### 2.2 접근성 보완 토큰 — 구현 시 우선

원본 색은 위 표에 보존한다. 아래 토큰은 **추가 구현 값**이며, Figma 원본을 수정한 것이 아니다. 대비는 불투명 단색의 WCAG 상대 휘도 기준 근삿값이다.

| 구현 의미 토큰 | 값 | 적용 및 대비 |
|---|---|---|
| `on-action` | `#000000` | 초록 CTA의 글자·아이콘. `#00D959` 위 약 **11.07:1** |
| `accent-text` | `#007A32` | 카드 이름·선택 칩 글자·링크. 흰색 위 **5.48:1**, accent-soft 위 **5.04:1** |
| `muted-text` | `#4D4D4E` | placeholder·오락용 안내·읽어야 하는 보조 문구. surface-sub 위 **7.82:1** |
| `danger-text` | `#C52C35` | 오류 문구·오류 경계. 흰색 위 **5.55:1** |
| `control-border` | `#7A837E` | 입력·Secondary·비선택 칩의 식별 가능한 경계. 흰색 위 **3.91:1**, bg 위 **3.53:1** |
| `focus-ring` | `#000000` | 키보드 포커스 외곽선. 초록·흰색·연회색 표면에서 구분 |

- 일반 텍스트 **4.5:1 이상**, 큰 텍스트(24 CSS px 이상 또는 약 18.67px 이상 Bold) **3:1 이상**. 필수 UI 경계·상태 표시는 인접색 대비 **3:1 이상**을 확보한다.
- 원본의 흰 글자/초록 배경은 **1.90:1**이다. 원본 설명의 “16 Bold 이상이면 가능”은 적용하지 않는다. 글자 크기만 키워 해결할 수 없으며 L/M 모두 `on-action`을 사용한다.
- 원본 tertiary/흰색은 **2.71:1**, danger/흰색은 **3.91:1**이므로 작은 안내·오류 텍스트에는 위 보완색을 사용한다.
- 선택 칩은 accent-soft 배경 + accent-text 글자·경계 + Bold + 선택 상태를 함께 사용한다. 초록 단색으로만 선택을 표현하지 않는다.
- 원본 accent 테두리만으로 입력 포커스를 표현하지 않는다. 검정 2px outline, 2px offset을 추가한다.
- 비활성 컨트롤은 대비 예외 대상이지만 읽기 쉽게 disabled 배경 + secondary 글자로 보완한다. 실제 비활성 동작과 상태를 함께 제공한다.
- 장식용 accent/accent-illust는 유지할 수 있다. 정보를 전달하는 글자·아이콘·상태 표시는 같은 예외로 취급하지 않는다.

## 3. 타이포그래피

**원본 공통:** `Noto Sans KR`, 자간 **-2%**(`letter-spacing: -0.02em`). 원본의 행간은 배수가 아니라 px다.

| Figma 스타일 | 두께 | 크기 / 행간 | 용도 |
|---|---|---|---|
| `Taro/Display` | Bold 700 | 28 / 38px | 시작 화면 타이틀 |
| `Taro/Title` | Bold 700 | 22 / 32px | 화면 질문 |
| `Taro/Headline` | Bold 700 | 18 / 26px | 카드 이름·앱바 |
| `Taro/Body` | Regular 400 | 16 / 26px | 해석·입력값·본문 |
| `Taro/Body Bold` | Bold 700 | 16 / 24px | L 버튼 |
| `Taro/Label` | Medium 500 | 15 / 22px | M 버튼·칩 기본·토스트 |
| `Taro/Caption` | Regular 400 | 13 / 19px | 안내·보조 |
| `Taro/Caption Bold` | Bold 700 | 13 / 19px | 입력 라벨 |

- 선택 칩은 원본에서 15px Bold 700으로 강조한다.
- 해석은 가운데 정렬, 최대 3줄·90자 이내. 1줄은 이름을 포함한 카드×주제 문장, 2줄은 별자리, 3줄은 전공 계열 문장이다.
- 전공 미입력 또는 계열 매칭 실패 시 3줄째를 숨긴다. 빈 줄이나 임의의 기본 전공 문장을 남기지 않는다.
- **구현 보완:** Noto Sans KR 400/500/700을 실제 로드하고 `system-ui, sans-serif`를 fallback으로 둔다. 폰트 로드가 끝난 후 저장 이미지를 생성한다.
- 긴 이름(최대 10자)·문장을 텍스트 클리핑이나 말줄임으로 감추지 않는다. 기본 화면 폭에서 3줄·90자 조건을 만족하는 짧은 문구를 사용하고 최장 사례를 검수한다. 작은 화면·확대 보기에서는 읽기와 전체 내용 노출을 우선하여 높이를 늘린다.

## 4. 레이아웃·간격·곡률

### 4.1 원본 확인값

- 기본 화면 **375×812px**, 결과 예시는 **375×876px**. 콘텐츠 좌우 여백 **20px**, 기본 콘텐츠 폭 **335px**.
- 시작 화면: 상단 44px / 하단 34px / 요소 간 24px.
- 앱바: **375×56px**, 좌우 padding 16px, 요소 gap 8px.
- 입력 화면 Body: 상단 8px / 좌우 20px / gap 16px.
- 입력 화면 하단 CTA: 상단 12px / 좌우 20px / 하단 34px.
- 결과 Body: 상단 4px / 좌우 20px / gap 14px. M 버튼 2열의 열 간격 **11px**, 행 사이 **14px**.
- 칩: 3열×2행, 가로·세로 gap **10px**. 105×44px 세 개 + 10px 간격 두 개 = 335px.
- 간격 실측에는 2, 4, 6, 8, 10, 11, 14, 16, 20, 24, 28px 등이 있다. 임의의 8px 배수 체계로 반올림하지 않는다.

| 요소 | 크기 / padding / gap | 곡률 |
|---|---|---|
| Button L | 335×56px, 아이콘-라벨 6px | 16px |
| Button M | 162×48px, 아이콘-라벨 6px | 14px |
| Input Field | 335×52px, 좌우 16px | 12px |
| Input 전체 | 기본 335×79px / 오류 335×106px, 라벨·필드·헬퍼 gap 8px | 필드 기준 |
| Topic Chip | 105×44px | 22px |
| Privacy Notice | 기본 335×85px, 상하 14px / 좌우 16px / gap 10px | 12px |
| Toast | 내용에 따라 너비 변경, 상하 14px / 좌우 20px, 한 줄 높이 50px | 12px |
| Tarot Card / Back | 120×200px, 바깥 2px 초록선·안쪽 1px선 | 12px / 안쪽 8px |
| Tarot Card / Front | 160×268px | 10px |
| Result Card | 원본 335×534px, 상하 28px / 좌우 24px / gap 16px | 24px |
| Reading 내부 | 287px 폭, 문장 사이 gap 2px | — |

- 원본 Front에만 확인된 그림자: `0 6px 16px 0 rgba(0,0,0,0.12)`. 나머지 주요 컴포넌트에는 효과가 없다. 기존의 ‘모든 그림자 금지’ 규칙은 폐기하되 그림자를 임의로 추가하지 않는다.

### 4.2 반응형·상태 구현 보완

원본에는 반응형 breakpoint·hover·pressed·loading의 별도 시안이 없다. 다음을 기본으로 한다.

- 기존 최대 폭 **430px 중앙 정렬**은 구현 정책으로 유지한다. 375px은 기준 시안이지 고정 viewport가 아니다.
- 앱 셸은 `width: 100%; max-width: 430px; min-height: 100dvh`. 콘텐츠는 좌우 20px, 버튼·입력은 사용 가능한 폭을 채운다.
- 2열 액션은 `repeat(2, minmax(0, 1fr))`, 칩은 3열 유동 폭을 기본으로 한다. 좁은 폭·확대에서 라벨이 잘리면 열 수를 줄이고 세로 스크롤을 허용한다.
- 44/34px은 시안의 상하 공간이다. 브라우저에서는 safe-area 환경값을 사용해 중복 합산을 피한다. 가상 키보드가 필드·오류·CTA를 가리지 않도록 스크롤을 허용한다.
- hover는 밑줄/경계 강조, pressed는 위치 변화 없이 내부 경계 강조를 기본으로 한다. 불투명도를 낮춰 글자 대비를 훼손하지 않는다.
- 이미지 생성·공유 처리 중 중복 실행을 막고 버튼에 진행 상태와 `aria-busy`를 제공한다. 완료·실패 시 다시 조작 가능하게 한다. 비동기 실패에도 결과를 지우지 않는다.

## 5. 컴포넌트 규칙

### 5.1 Button

원본 `Button`(`3:98`): `Type=Primary|Secondary|Disabled`, `Size=L|M`. 노출 속성은 `Label`, `Show Icon`, `Icon`이다.

| Type | 원본 | 접근성 우선 구현 |
|---|---|---|
| Primary | accent 배경 + 흰 글자 | accent 배경 + 검정 글자·아이콘 |
| Secondary | surface 배경 + primary 글자 + border 1px | 글자는 유지, 경계는 control-border 1px |
| Disabled | disabled 배경 + 흰 글자 | disabled 배경 + secondary 글자, 실제 disabled 처리 |

- L: 화면당 주요 행동 1개. 시작 화면 [타로 시작], 입력 완료 후 [카드 한 장 뽑기].
- M: 결과 2×2 액션. 위 행 [이미지 저장](Secondary) / [결과 공유](Primary), 아래 행 [다시 뽑기] / [처음으로](둘 다 Secondary).
- 아이콘은 20px, 라벨과 6px 간격. icon-only 버튼은 접근 가능한 이름과 최소 44×44px 조작 영역을 제공한다.
- 원본에 Ghost·Muted variant는 없다. 이전 가이드의 variant를 새 팩의 기준으로 사용하지 않는다.

### 5.2 Input / Form

원본 `Input`(`3:124`): `State=Default|Filled|Focused|Error`, 속성 `Label`, `Value`, `Helper`.

| 상태 | 원본 경계·글자 | 구현 적용 |
|---|---|---|
| Default | border 1px, tertiary placeholder | control-border 1px, muted-text placeholder |
| Filled | border 1px, primary 입력값 | control-border 1px, 입력값 유지 |
| Focused | accent 2px, primary 입력값 | 원본 경계 + 검정 2px outline/2px offset |
| Error | danger 1.5px + Caption 오류 문구 | danger-text 1.5px + 같은 색 헬퍼, 색 외 문구도 표시 |

- 라벨은 Caption Bold, 입력값은 Body, Field는 surface 배경·높이 52px·곡률 12px다. 기본 상태 Helper는 숨기고 Error에서만 표시한다.
- 이름 필수·최대 10자·닉네임 권장. 생년월일 필수·실제 존재하는 날짜만 허용. 예시 표시 `YYYY . MM . DD`.
- 전공 선택. 인문·사회·경영·자연·공학·예체능 6계열로 매칭하며 실패하면 전공 문장을 생략한다.
- 이름·유효한 생년월일·주제 하나가 모두 있어야 CTA를 활성화한다. 오류 날짜도 비활성 조건에 포함한다.
- 오류 문구: **날짜를 다시 확인해 주세요**. 라벨과 입력을 연결하고 오류는 `aria-invalid` 및 `aria-describedby`로 연결한다. placeholder를 라벨 대신 쓰지 않는다.

### 5.3 Topic Chip

원본 `Topic Chip`(`3:103`): `State=Default|Selected`, `Label` 속성.

- 커리어 / 재물 / 연애 / 건강 / 학업 / 종합의 **단일 선택**.
- Default: 흰 배경 + secondary 글자, 원본 1px border → 구현 control-border.
- Selected: accent-soft 배경 + Bold 글자, 원본 1.5px accent 경계·accent-strong 글자 → 구현 accent-text 경계·글자.
- radio group 의미 구조와 키보드 이동·선택 상태를 제공한다.

### 5.4 App Bar · Privacy Notice · Toast · Icons

- `App Bar`(`3:133`): `Title`, `Show Back`. 56px 높이, Headline, 20px 뒤로가기 아이콘. 조작 영역은 44px 이상으로 확장하되 시각 크기는 유지한다.
- `Privacy Notice`(`3:125`): `Text`. surface-sub, lock 아이콘 20px, Caption secondary. 고정 높이로 자르지 않고 내용에 맞춰 늘린다.
- 입력 화면 개인정보 안내 원문:
  > 입력한 이름 · 생년월일 · 전공은 해석을 만드는 데만 쓰고, 서버로 보내거나 저장하지 않아요. 창을 닫거나 [처음으로]를 누르면 바로 지워져요.
- 결과 화면 축약 안내:
  > 정보는 저장되지 않아요. [처음으로]를 누르면 바로 지워져요.
- `Toast`(`3:131`): `Text`. inverse 배경 + 흰 Label, 곡률 12px. 원본은 2초 후 사라짐. 하단 safe-area와 겹치지 않게 배치하고 긴 문구는 줄바꿈한다. `role=status`/polite로 알리며 중요한 실패 해결 수단을 토스트에만 두지 않는다.
- 아이콘 원본: `chevron-left`, `download`, `share`, `refresh`, `home`, `lock`, `copy`. SVG로 구현한다. 장식 아이콘은 접근성 트리에서 제외한다. 화면 예시의 emoji는 UI 아이콘 대체용이며 공유 메시지의 🔮와는 구분한다.

### 5.5 Tarot Card / Back · Front · Deck

- Back(`3:139`): 직접 제작한 뒷면 그래픽. 뽑기 전·뒤집기 시작에 사용한다.
- Front(`3:146`): `Art` 이미지 fill을 선택 카드로 교체. 기본은 XIX 태양. 아트워크를 임의의 그라데이션·emoji로 대체하지 않는다.
- 원본 Deck은 메이저 아르카나 **00 The Fool ~ 21 The World 22장**. 무작위 한 장·정방향만 사용한다. 개별 Front 자산은 160×268px 계열이다.
- 원본 표기 출처: **78 Tarot Cards (Community) · Rider-Waite-Smith (1909) 퍼블릭 도메인 그림**. 이는 팩의 출처 표기를 옮긴 것이며 배포 지역별 권리나 디지털 이미지 라이선스를 별도로 검증한 것은 아니다. 출시 전 원본 링크·파일 이용 조건을 확인하고 자산과 함께 출처를 보관한다.

### 5.6 Result Card — 화면용

원본 `Result Card`(`3:153`)는 **335×534px**, 흰 배경·곡률 24px·상하 28px/좌우 24px·gap 16px다.

위에서 아래로:
1. `{이름}님의 타로 · {주제}` — Caption Bold, secondary.
2. Front 아트워크 — 160×268px.
3. `{카드 이름} · {별자리}` — Headline, 원본 accent-strong → 구현 accent-text.
4. 해석 문장 최대 3개 — Body 가운데 정렬, 문장 사이 2px.
5. `※ 오락용 타로 해석입니다` — Caption, 원본 tertiary → 구현 muted-text.

속성: `Title`, `Meta`, `Line 1`, `Line 2`, `Line 3`, `Show Major Line`. 전공 문장 생략 시 `Show Major Line=false`에 해당하는 처리를 한다. 화면 카드의 높이는 내용에 따라 늘어날 수 있다.

## 6. 화면·동작 매핑

| 화면 | 내용 / 주요 행동 |
|---|---|
| S-01 · F-1 | 오늘의 타로, 카드 뒷면, 소개, L Primary [타로 시작], 오락용·미저장 안내 |
| S-02 · F-2 | 앱바, 이름·생년월일·전공, 주제 6개, 개인정보 안내, L CTA |
| S-02-A | 필수값이 유효하면 CTA 활성; 오류 시 필드 아래 메시지 |
| S-03-P · F-3 | 좌우 스와이프 카드덱, 탭할 카드 선택 |
| S-03-P2 / D | 선택 카드 가운데 이동 → 뒤집기 → 공개 |
| S-03 · F-4~7 | 결과 카드, 2×2 M 액션, 개인정보 안내 |
| S-03-S | 저장 실패: 이미지와 길게 눌러 저장 안내·닫기 |
| S-03-C | 공유 메뉴 없음: 자동 복사 후 결과 유지·토스트 |
| 복사 실패 | 메시지 원문을 선택 가능한 형태로 표시·닫기 |

### 6.1 카드 선택 모션 — 원본 가이드

- 22장 뒷면의 부채꼴: 반지름 **430px**, 간격 **8°**. 화면에는 일부 카드만 보인다.
- 진입: 아래→위, 중앙 기준 stagger **0.02s**.
- 스와이프: wheel 하나만 회전, `quickTo 0.45s`; 놓으면 속도를 반영한 후 **8° 스냅**.
- 탭: 선택 카드 중앙 이동 **0.5s**, scale **1.7** → Y축 뒤집기 **180° / 0.6s**.
- 결과 자리로 FLIP **0.5s** → 해석 줄 stagger **0.08s**.
- `transform`, `opacity`만 애니메이션. 0.6s는 뒤집기 구간이며 전체 시퀀스를 1초 이내라고 오해하지 않는다. 화면 예시에는 뒤집기 후 0.4s 뒤 결과 전환도 표기되어 있어, 구현에서는 상세 모션 가이드의 단계 정의를 우선한다.
- 원본 reduced-motion은 4배속이다. **접근성 보완으로는 회전·이동·스태거를 생략하고 즉시 결과를 표시**한다. 동작 의미와 카드 결과는 동일하게 유지한다.
- **구현 보완:** 스와이프 외에도 이전/다음·키보드로 선택할 수 있게 한다. 선택 확정 후 중복 탭을 막고 공개 결과를 보조기술에 알린다.

### 6.2 저장·공유·재시작

| 상황 | 처리 / 문구 |
|---|---|
| 저장 성공 | `이미지를 저장했어요` |
| 저장 실패·인앱 제약 | 저장 이미지 표시 + `이미지를 길게 눌러 저장해 주세요` + 닫기 |
| 기기 공유 지원 | 이미지+글 공유를 우선; 완료·취소 모두 결과 유지 |
| 공유 메뉴 없음 | 글 자동 복사 + `결과를 복사했어요. 원하는 앱에 붙여 넣어 주세요` |
| 복사 실패 | 선택 가능한 공유 글 + `아래 글을 길게 눌러 복사해 주세요` + 닫기 |
| 다시 뽑기 | 입력 정보 유지, S-02 주제 선택부터 |
| 처음으로 | 이름·생년월일·전공·주제·결과 모두 삭제 후 S-01 |

- 수동 저장·복사 UI는 사용자가 닫을 때까지 유지한다. 닫기 후 포커스를 호출 버튼으로 돌린다. modal은 제목·focus trap·Escape 닫기를 제공한다.
- 개인정보·결과는 메모리에서만 사용한다. 서버·AI·분석 도구 전송, localStorage·쿠키 저장 없음. 새로 고침·창 닫기·처음으로 시 삭제한다.

공유 메시지:

```text
🔮 {이름}님의 타로 · {주제}
{카드 이름} · {별자리}
{해석 최대 3줄}
※ 오락용 타로 해석입니다
나도 한 장 뽑기 → {시작 링크}
```

생년월일·전공 원문을 넣지 않는다. 전공 계열 해석은 포함할 수 있다. 링크는 시작 화면이며 이름·입력 정보·결과를 URL에 담지 않는다.

## 7. 1080×1350 전용 저장 레이아웃 — 승인된 보완

**화면 카드와 저장 이미지를 구분한다.** 원본 화면 카드 335×534는 4:5가 아니므로 단순 확대·강제 리사이즈·잘라내기로 1080×1350을 만들지 않는다. 저장용은 같은 데이터와 디자인 언어를 쓰는 별도 고정 캔버스로 재배치한다. 원본에는 이 규격의 완성 프레임이 없으므로 다음 좌표는 새 구현 기준이다.

- 출력: **1080×1350px PNG**, 불투명 흰 배경. 앱바·버튼·개인정보 패널은 제외한다.
- 캔버스 좌우 기본 안전 여백 **72px**, 모든 글자는 최대 **936px** 안에 둔다.
- 텍스트는 Noto Sans KR, 자간 -2%, 가운데 정렬. 색상은 접근성 보완을 적용한다.
- 필수 내용: 이름·주제·카드 그림·카드 이름·별자리·해석·오락용 안내·하단 **오늘의 타로**.

| 영역 | 저장 캔버스 배치 | 서체 / 색 |
|---|---|---|
| 이름·주제 | x=72, y=64, w=936, h=54 | 36/54px Bold, secondary |
| 카드 그림 | x=380, y=144, w=320, h=536 | Front 160:268 비율 유지, 곡률 20px |
| 카드 이름·별자리 | x=72, y=712, w=936, h=78 | 54/78px Bold, accent-text |
| 해석 영역 | x=72, y=826, w=936, h=320 | 36/48px Regular, primary |
| 오락용 안내 | x=72, y=1170, w=936, h=54 | 36/54px Regular, muted-text |
| 서비스 이름 | x=72, y=1240, w=936, h=54 | 36/54px Bold, secondary |

- 해석은 최대 3문장·90자 이내를 유지한다. 저장용에서는 각 문장을 최대 2개의 시각적 줄로 표시하고 문장 사이 16px을 둔다. 최대 6×48+2×16=320px 안에서 전체 내용을 보존한다.
- 90자 제한만으로 각 영역에 들어간다고 보장하지 않는다. 실제 폰트로 측정하고, 긴 카드명·10자 이름·전공 문장 유무를 검사한다. 넘치면 준비된 짧은 문구를 사용한다. 임의 잘라내기·비균등 축소·개인정보/오락용 안내 생략은 금지한다.
- 캔버스 외곽은 흰 사각형으로 채워 투명 모서리·배경색 차이 문제를 피한다. 화면용 Result Card의 곡률 24px을 PNG 전체에 기계적으로 확대 적용하지 않는다.
- 생년월일·전공 원문은 이미지에 넣지 않는다. 이미지와 공유 글은 화면에 표시한 동일 결과 데이터에서 생성한다.
- 폰트·이미지 준비 후 내보내고, 최종 PNG의 실제 픽셀 크기·텍스트 누락·그림 비율을 확인한다. **1080×1350은 4:5 피드형 이미지이며 9:16 스토리 규격은 아니다.**

## 8. Tailwind CSS v4 / shadcn/ui 매핑 예시

아래는 구현 참고용이며 저장소에 실제 스타일 파일을 추가한 것은 아니다. 원본 토큰과 접근성 의미 토큰을 섞어 덮어쓰지 않는다.

```css
@theme {
  --font-sans: 'Noto Sans KR', system-ui, sans-serif;
  /* Figma 원본 */
  --color-taro-bg: #f3f3f5;
  --color-taro-surface: #ffffff;
  --color-taro-surface-sub: #f6f6f8;
  --color-taro-text-primary: #000000;
  --color-taro-text-secondary: #4d4d4e;
  --color-taro-text-tertiary: #979f9b;
  --color-taro-on-accent: #ffffff;
  --color-taro-border: #dcdcdd;
  --color-taro-accent: #00d959;
  --color-taro-accent-soft: #e6faef;
  --color-taro-accent-strong: #00d959;
  --color-taro-disabled: #d7d7d7;
  --color-taro-danger: #e5484d;
  --color-taro-inverse: #232427;
  --color-taro-accent-illust: #00de00;
  /* 접근성 보완 */
  --color-taro-on-action: #000000;
  --color-taro-accent-text: #007a32;
  --color-taro-muted-text: #4d4d4e;
  --color-taro-danger-text: #c52c35;
  --color-taro-control-border: #7a837e;
  --color-taro-focus-ring: #000000;
  /* 원본 실측을 구현 토큰으로 명명 */
  --radius-button-l: 16px;
  --radius-button-m: 14px;
  --radius-field: 12px;
  --radius-chip: 22px;
  --radius-result: 24px;
  --radius-notice: 12px;
  --radius-toast: 12px;
}

:root {
  color-scheme: light;
  --background: var(--color-taro-bg);
  --foreground: var(--color-taro-text-primary);
  --card: var(--color-taro-surface);
  --card-foreground: var(--color-taro-text-primary);
  --popover: var(--color-taro-surface);
  --popover-foreground: var(--color-taro-text-primary);
  --primary: var(--color-taro-accent);
  --primary-foreground: var(--color-taro-on-action);
  --secondary: var(--color-taro-surface);
  --secondary-foreground: var(--color-taro-text-primary);
  --muted: var(--color-taro-surface-sub);
  --muted-foreground: var(--color-taro-muted-text);
  --accent: var(--color-taro-accent-soft);
  --accent-foreground: var(--color-taro-accent-text);
  --destructive: var(--color-taro-danger-text);
  --destructive-foreground: #ffffff;
  --border: var(--color-taro-control-border);
  --input: var(--color-taro-control-border);
  --ring: var(--color-taro-focus-ring);
  --radius: 0.75rem;
}

body {
  margin: 0;
  background: var(--background);
  color: var(--foreground);
  font-family: var(--font-sans);
  letter-spacing: -0.02em;
}
.taro-shell { width: 100%; max-width: 430px; margin-inline: auto; min-height: 100dvh; }
.taro-content { padding-inline: 20px; }
.taro-actions { display: grid; grid-template-columns: repeat(2, minmax(0, 1fr)); gap: 14px 11px; }
.taro-topics { display: grid; grid-template-columns: repeat(3, minmax(0, 1fr)); gap: 10px; }
.taro-action-primary { background: var(--primary); color: var(--primary-foreground); }
:where(button, input, a, [tabindex]):focus-visible {
  outline: 2px solid var(--ring);
  outline-offset: 2px;
}
@media (prefers-reduced-motion: reduce) {
  .taro-deck, .taro-deck *, .taro-reading, .taro-reading * {
    animation: none !important;
    transition: none !important;
  }
}
```

shadcn/ui の汎用 `--radius` 하나로 모든 컴포넌트를 맞추지 말고 Button L/M·Field·Result에 해당 곡률을 명시한다. 프로젝트의 Tailwind/shadcn 버전이 요구하는 변수 연결 방식에 맞춰 통합하고, 다크 모드 자동 적용은 하지 않는다. reduced-motion에서는 CSS뿐 아니라 동작 제어에서도 최종 결과 상태를 즉시 설정해야 한다.

## 9. 인수 체크리스트와 남은 확인

### 구현 인수 기준

- [ ] 원본 15색·8개 텍스트 스타일이 문서와 일치하며, 실제 UI는 접근성 의미 토큰을 사용한다.
- [ ] 375px 기준 원본 간격·L/M 크기·곡률을 재현한다. 결과 Primary는 공유 하나뿐이다.
- [ ] 320/375/430px 및 200% 확대에서 내용·포커스·CTA가 잘리지 않는다.
- [ ] 키보드만으로 입력·주제·덱 선택·모달 닫기·재시작이 가능하다.
- [ ] 입력 오류·선택·진행 상태를 색상 외 방식으로도 전달한다.
- [ ] reduced-motion에서 회전·부채꼴 이동 없이 동일 결과를 확인한다.
- [ ] 최대 10자 이름·긴 카드명·전공 미입력/미매칭·잘못된 날짜를 검사한다.
- [ ] PNG가 실제 1080×1350이며 서비스 이름·오락용 안내·해석 전체가 보인다.
- [ ] 저장/공유/복사 실패 fallback과 공유 취소에서 결과가 유지된다.
- [ ] 저장 이미지·공유 글·URL에 생년월일·전공 원문이 없다.
- [ ] 처음으로·새로 고침 후 입력과 결과가 사라지고 서버/저장소/분석 전송이 없다.

### 원본과의 차이 및 출시 전 확인

- 접근성 보완 색상·포커스·키보드·감소된 모션과 전용 저장 레이아웃은 이 문서의 구현 기준이다. **Figma 원본은 이번 작업에서 변경하지 않았다.** 향후 디자인 팩에도 동기화해야 한다.
- 팩의 원본 Result Card에는 별도 서비스 이름이 없고 4:5도 아니다. 사용자 승인에 따라 저장 이미지에만 7절 전용 레이아웃과 ‘오늘의 타로’를 추가했다.
- 카드 그림의 정확한 Community 원본 URL·디지털 자산 이용 조건, 실제 서비스 시작 URL은 확인 후 자산/배포 설정에 기록한다. 출처명만으로 이용 허가를 단정하지 않는다.
- PRD의 지표 목표·문구 범위 검토·개인정보 동의 필요 여부 등 제품/법무 미정 사항을 이 문서로 임의 확정하지 않는다. 현재 기능명세와 팩의 6개 주제·22장 기준을 유지한다.

이 체크리스트는 **앞으로의 구현 검수 항목**이며, 문서 갱신만으로 앱의 접근성·이미지 출력·개인정보 동작이 검증되었다는 뜻은 아니다.
