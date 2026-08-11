# 🚀 Transformer & KV Cache H/W Seminar

오프라인 환경에서 100% 독립 동작하도록 설계된 **트랜스포머 아키텍처 & KV Cache 하드웨어 세미나 웹 프레젠테이션** 자료입니다.

---

## 📁 Git 커밋 및 파일 경로 안내

다른 PC에서 인터넷 연결 없이 프레젠테이션을 실행하려면 **모든 필수 파일이 동일한 단일 폴더(디렉토리) 내에 위치**해야 합니다.

### 1. Git에 반드시 올라가야 하는 필수 파일 목록 (총 4개)

```
c:\python\AI_Seminar\ (프로젝트 루트 디렉토리)
 ├── transformer_seminar_new.html   <-- 메인 세미나 슬라이드 웹 문서
 ├── katex.min.css                  <-- [필수] 오프라인 수식 CSS
 ├── katex.min.js                   <-- [필수] 오프라인 수식 엔진 JS
 └── auto-render.min.js             <-- [필수] 오프라인 수식 자동 파서 JS
```

> ⚠️ **주의사항:** `katex.min.css`, `katex.min.js`, `auto-render.min.js` 3개 파일이 `transformer_seminar_new.html`과 **같은 폴더**에 있지 않으면 수식이 렌더링되지 않고 깨질 수 있습니다.

---

## 💻 다른 PC에서 다운로드 및 오프라인 실행 방법

1. **Git Clone / Zip 다운로드**
   ```bash
   git clone <사용자_Git_리포지토리_URL>
   cd AI_Seminar
   ```
2. **오프라인 실행**
   - 별도의 웹 서버(Nginx, Apache 등)나 Python/Node.js 실행이 **전혀 필요 없습니다**.
   - `transformer_seminar_new.html` 파일에서 마우스 우클릭 ➔ **[연결 프로그램]** ➔ **Chrome / Edge / Safari / Firefox 브라우저**로 직접 열어서 바로 프레젠테이션을 시작하세요.

---

## ⌨️ 프레젠테이션 키보드 조작법

| 기능 | 키보드 단축키 / 클릭 |
|---|---|
| **다음 슬라이드** | `→` (오른쪽 화살표) / `Spacebar` / 하단 **[다음 (Next)]** 버튼 |
| **이전 슬라이드** | `←` (왼쪽 화살표) / 하단 **[이전 (Prev)]** 버튼 |
| **목차 (Index) 팝업** | 상단 우측 **[📋 목차 (Index)]** 버튼 |
| **발표자 노티 Toggle** | 상단 우측 **[💡 노티 (Notes)]** 버튼 |
| **전체화면 모드** | 상단 우측 **[🖥️ 전체화면]** 버튼 |
| **팝업 닫기** | `Esc` 키 |

---

## 📚 세미나 전체 내용 요약 (Total 41 Slides)

본 세미나는 문과적 직관 비유와 구체적인 수치 연산을 결합하여 LLM의 핵심 동작과 H/W 병목 원리를 설명합니다.

1. **단어 임베딩 (Embedding)**
   - 단어를 다차원 공간의 수치 벡터로 변환 ($d_{model}$)
   - `King - Man + Woman = Queen` 벡터 연산의 원리와 수치적 직관
2. **거리(Distance) vs 유사도(Similarity)**
   - 유클리드 거리 ($L_2$), 맨해튼 거리 ($L_1$), 코사인 유사도 ($\cos\theta$) 비교
   - 왜 트랜스포머는 **Dot Product (내적)**을 사용하는가? (수학적 시그널 강도 + H/W GEMM/MAC 100% 가속)
3. **Q, K, V 분신 투영 & Self-Attention 수치 연산**
   - 문장 *"I LOVE YOU"*의 구체적 $4 \times 2$ 가중치 투영 과정
   - **Query (질문)**, **Key (열쇠)**, **Value (실물 재료)** 역할 및 4단계 어텐션 파이프라인
4. **Softmax & 딥러닝 미분의 비밀**
   - 거친 점수를 합이 1.0(100%)인 확률 비율로 변환하는 정규화
   - 왜 하필 자연상수 $e^x$를 쓰는가? (미분해도 자기 자신 $\rightarrow$ NPU/GPU 역전파 역량 가속)
5. **Prefill vs Decoding Phase & KV Cache H/W 혁신**
   - **Prefill (Compute-Bound)**: 입력 프롬프트 대규모 GEMM 연산
   - **Decoding (Memory-Bound)**: 토큰 1개씩 생성시 $O(N^2)$ 재계산 비극 방지를 위한 **KV Cache** 도입
6. **HBM 메모리 경제학 & 반도체 최적화**
   - 학습(Training) vs 추론(Serving) 메모리 점유 구조 차이
   - HBM 용량(Capacity) vs HBM 대역폭(Bandwidth) 병목
   - **FlashAttention**, **PagedAttention**, **KV Cache Quantization (INT8/INT4)** 최신 H/W 최적화 3대장
