# 🎨 세미나 프레젠테이션 제작 표준 지침서 (Seminar Design & Pedagogy Guidelines)

본 지침서는 **AI 에이전트 및 팀 개발자가 향후 트랜스포머, AI 하드웨어, 딥러닝 세미나 프레젠테이션 자료를 추가/확장할 때 반드시 준수해야 하는 디자인, 내용 구조, 전개 방식의 핵심 가이드라인**입니다.

---

## 📌 1. 슬라이드 구성 4대 철학 (Core Pedagogy Rules)

### 1️⃣ One-Page, One-Concept (한 페이지 = 한 개념 원칙)
- **금지 사항**: 단 한 슬라이드에 수식, 코드, 복잡한 비유, 여러 단계의 다이어그램을 과도하게 쑤셔 넣는 것을 엄격히 금지합니다.
- **슬라이드 분량 넉넉히 확장**: 설명할 내용이 많으면 슬라이드 개수를 저축하지 말고 **`[개념 1/3]`, `[개념 2/3]`, `[개념 3/3]` 형태로 슬라이드를 대폭 늘려서 차근차근(Step by Step) 전개**하세요.

### 2️⃣ Step-by-Step 연속성 및 이전 개념 복습 (Recap & Connect)
- 새 슬라이드가 시작될 때는 이전 슬라이드에서 유도된 핵심 수치나 결론(예: *"앞 슬라이드에서 구한 'I'의 어텐션 점수 [1, 0, 1] 기억나시나요?"*)을 상단에서 **자연스럽게 한 줄 복습(Recap)**하며 시작하세요.
- 앞 슬라이드의 개념이 다음 슬라이드의 하드웨어/수식 연산으로 연결되는 파이프라인 흐름을 직관적으로 보여주어야 합니다.

### 3️⃣ 수식의 1:1 실전 수치 풀이화 (Math-to-Numeric Code)
- 추상적인 수학 기호($\sum, W^Q, QK^T$)만 던져두지 마세요.
- **반드시 실제 수치 벡터 예시($X_{\text{VERY}} = [1,0,0,1]$, $Q=[1,0]$ 등)**와 $4 \times 2$ 행렬 곱산 풀이 카드를 함께 배치하여, 청중이 손으로 따라갈 수 있게 1:1 수치 풀이를 보여주어야 합니다.

### 4️⃣ "💡 문과적 직관 해석" 박스 필수 포함 (Human-Note Box)
- 수식과 기술 카드가 포함된 모든 슬라이드 하단에는 **반드시 비전공자/입문자도 0.1초 만에 감을 잡을 수 있는 노란색 직관 비유 박스**를 삽입하세요.
  - *예시*: `"Softmax는 지저분한 점수를 합이 100%인 확률 지시서로 다듬어주는 예쁜 다듬기 기계입니다!"`

---

## 🎨 2. 디자인 테마 & UI/UX 디자인 시스템

### 1️⃣ Dark Glassmorphism 톤앤매너
- **배경색 (Background)**: `#070a12` (딥 다크 블루/블랙) + 은은한 래디얼 그라데이션
- **카드 배경 (Card BG)**: `rgba(18, 26, 43, 0.85)` + `backdrop-filter: blur(16px)`
- **카드 테두리**: `border: 1px solid rgba(255, 255, 255, 0.12)`

### 2️⃣ 퍼스널 컬러 시스템 (Color-Coding Standard)
개념별로 아래 지정된 CSS 변수를 엄격히 준수하여 청중의 시각적 직관을 돕습니다:

| 요소 구분 | CSS 변수명 | 색상 코드 | 시각적 의미 |
|---|---|---|---|
| **Query (질문)** | `--q-color` | `#38bdf8` (Cyan/Blue) | 질문표, 입력 토큰, Prefill |
| **Key (열쇠)** | `--k-color` | `#34d399` (Emerald Green) | 검제 열쇠, Key Cache |
| **Value (재료)** | `--v-color` | `#c084fc` (Purple) | 실물 문맥 의미 데이터, Value Cache |
| **Attention / Score** | `--score-color` | `#fbbf24` (Amber/Gold) | Softmax 확률, 가중합, 직관 박스 |
| **H/W Memory / Alert** | `--hw-color` | `#f43f5e` (Rose/Red) | HBM 대역폭, 병목 경고, 재계산 비극 |

### 3️⃣ 화면 비율 & 여백 규격 (Viewport Boundaries)
슬라이드가 전체화면 모드에서도 위쪽으로 쏠리거나 하단 이동 버튼(`nav-controls`)과 겹치지 않도록 아래 margin 규격을 고정합니다:
```css
.slide-container {
    position: relative;
    width: 92vw;
    max-width: 1280px;
    height: calc(100vh - 160px);
    max-height: 820px;
    margin: 55px auto 85px auto; /* 하단 네비게이션 공간 확보 */
}
```

---

## ⚙️ 3. 오프라인 100% 독립 실행 원칙 (Offline Infrastructure)

1. **CDN 사용 0%**: 외부 웹 CDN(`https://...`)을 통한 수식/스크립트 로드는 절대 금지합니다.
2. **로컬 상대 경로 렌더링**:
   ```html
   <link rel="stylesheet" href="./katex.min.css">
   <script defer src="./katex.min.js"></script>
   <script defer src="./auto-render.min.js"></script>
   ```
3. **독립 1파일 구동**: 별도의 Nginx/Python 웹 서버 없이 마우스 우클릭 ➔ 브라우저 열기만으로 구동 가능해야 합니다.

---

## 📑 4. 슬라이드 코드 기본 템플릿 (Slide HTML Template)

새 슬라이드를 추가할 때는 반드시 다음 HTML 구조를 기본 뼈대로 사용하세요:

```html
<!-- Slide N: [슬라이드 제목] -->
<div class="slide">
    <div class="slide-header">
        <div class="slide-title">
            <span>N. [주제] 슬라이드 제목 입력</span>
            <span class="slide-title-tag tag-concept">Tag Name</span>
        </div>
    </div>
    <div class="slide-body">
        <!-- 이전 슬라이드 연결 및 요약 문장 -->
        <p>슬라이드의 핵심 주제 및 이전 단계 연결 문장 입력</p>

        <!-- 핵심 정보 카드 2열 그리드 -->
        <div class="grid-2col">
            <div class="info-card card-q">
                <div class="card-title">1️⃣ 첫 번째 핵심 수치/개념</div>
                <p style="font-size: 0.85rem;">세부 수치 및 설명</p>
            </div>
            <div class="info-card card-k">
                <div class="card-title">2️⃣ 두 번째 핵심 수치/개념</div>
                <p style="font-size: 0.85rem;">세부 수치 및 설명</p>
            </div>
        </div>

        <!-- 💡 문과적 직관 해석 박스 (필수) -->
        <div class="human-note">
            💡 <b>문과적 직관 해석:</b> "일상 언어 비유로 쉬운 해석 문장 입력"
        </div>

        <!-- 💡 발표자 노티 (Speaker Note) -->
        <div class="speaker-note">
            💡 <b>발표 팁:</b> 발표자가 다음 슬라이드로 연결할 멘트 가이드
        </div>
    </div>
</div>
```

---

*이 가이드라인을 준수하여 제작된 프레젠테이션은 시각적 프리미엄 감성과 정교한 교육적 전달력을 100% 보장합니다.*
