# Project-Specific Agent Rules for AI Seminar Project

## 🎨 세미나 슬라이드 및 웹 프레젠테이션 제작 표준 지침

이 프로젝트에서 세미나 프레젠테이션(HTML/CSS/JS)을 수정, 보완, 생성할 때 반드시 다음 지침을 준수하세요. 세부 규격은 [SEMINAR_DESIGN_GUIDE.md](file:///c:/python/AI_Seminar/SEMINAR_DESIGN_GUIDE.md)를 참조하세요.

1. **One-Page, One-Concept 원칙**:
   - 한 슬라이드에 너무 많은 정보나 수식을 쑤셔 넣지 마세요.
   - 설명이 길어지면 `[슬라이드 1/3]`, `[슬라이드 2/3]` 형태로 슬라이드 개수를 넉넉히 늘려 차근차근(Step by Step) 전개하세요.

2. **이전 개념 연결 및 복습 (Recap & Connect)**:
   - 슬라이드가 시작할 때 이전 슬라이드에서 유도된 핵심 수치/결론을 상단에서 가볍게 복습(Recap)해주어 맥락을 이어가세요.

3. **수식의 1:1 수치 풀이화**:
   - 추상적 기호($\sum, QK^T$)만 제시하지 말고, $X_{\text{VERY}} = [1,0,0,1]$, $Q = [1,0]$ 등 구체적인 수치 벡터와 $4 \times 2$ 행렬 연산 카드를 배치하세요.

4. **"💡 문과적 직관 해석" 박스 필수 포함**:
   - 모든 기술 슬라이드 하단에는 비전공자도 0.1초 만에 이해하는 노란색 직관 비유 박스(`div.human-note`)를 포함하세요.

5. **컬러 톤앤매너 고수**:
   - Query (Cyan `#38bdf8`), Key (Emerald `#34d399`), Value (Purple `#c084fc`), Attention/Score (Amber `#fbbf24`), H/W Memory (Rose `#f43f5e`).

6. **100% 오프라인 동작 보장**:
   - 외부 CDN 자산을 절대 사용하지 말고, 로컬 `katex.min.css`, `katex.min.js`, `auto-render.min.js` 상대 경로를 사용하세요.
