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

## 📚 세미나 전체 내용 요약 (Total 44 Slides)

본 세미나는 문과적 직관 비유와 구체적인 수치 연산을 결합하여 LLM의 핵심 동작과 H/W 병목 원리를 설명합니다.

1. **단어 임베딩 (Embedding) (Slide 1~3)**
   - 단어를 다차원 공간의 수치 벡터로 변환 ($d_{model}$)
   - `King - Man + Woman = Queen` $[0.1, 0.9, 0.9, 0.7]$ 벡터 덧셈/뺄셈 연산의 수치적 직관
2. **거리(Distance) vs 유사도(Similarity) (Slide 4~10)**
   - 유클리드 거리 ($L_2$), 맨해튼 거리 ($L_1$), 코사인 유사도 ($\cos\theta$) 수치 풀이 비교
   - 왜 트랜스포머는 **Dot Product (내적)**을 사용하는가? (수학적 시그널 강도 + H/W GEMM/MAC 100% 가속)
3. **Q, K, V 분신 투영 & Self-Attention 수치 연산 (Slide 11~23)**
   - 문장 *"I LOVE YOU"*의 구체적 $4 \times 2$ 가중치 투영 과정
   - **Query (질문)**, **Key (열쇠)**, **Value (실물 재료)** 역할 및 4단계 어텐션 파이프라인
   - 전체 문장 $QK^T \cdot V$ 통합 행렬 연산
4. **Softmax & 딥러닝 미분의 비밀 (Slide 24~26)**
   - 거친 점수를 합이 1.0(100%)인 확률 비율로 변환하는 정규화
   - 왜 하필 자연상수 $e^x$를 쓰는가? (미분해도 자기 자신 $\rightarrow$ NPU/GPU 역전파 역량 가속)
5. **$\sqrt{d_k}$ 스케일링 & 단어별 맥락 벡터 연산 (Slide 27~31)**
   - 스케일링 미적용 시 내적 분산 폭발로 인한 One-Hot 쏠림(99.999%) 및 기울기 소멸 방지.
   - 단어 'I', 'LOVE', 'YOU' 단어별 맥락 벡터 ($[0.16, 0.42]$ 등) 및 Softmax 적용 전/후 1:1 비교.
6. **LLM 추론 로드맵 & HBM 상주 메모리 구조 (Slide 32~33)**
   - **LLM Master Map (Slide 32)**: 프롬프트 입력 $\rightarrow$ Prefill Phase $\rightarrow$ Decoding Phase 전체 파이프라인 로드맵.
   - **HBM 거주자 2대장 (Slide 33)**: **고정 상주 모델 가중치 (Model Weights ~140GB)** vs **동적 누적 KV Cache** 공존 구조.
7. **Decoding 단계 & $Q_{\text{VERY}}$ 1:1 수치 풀이 (Slide 34~36)**
   - **$Q_{\text{VERY}}$ 출처 (Slide 34)**: "I LOVE YOU" 어텐션 결과 LLM이 스스로 예측해낸 **1번째 생성 토큰 "VERY"** 및 임베딩 $X_{\text{VERY}}=[1,0,0,1]$ 질문 투영 수치 연산 ($Q_{\text{VERY}} = [1,0]$).
   - **Row 4 Append (Slide 35)**: $K_{\text{VERY}}([1,0]), V_{\text{VERY}}([0,1])$ 투영 수치 및 HBM 4번째 줄 Append 시각화.
   - **Decoding 어텐션 (Slide 36)**: $Q_{\text{VERY}}$가 HBM 4줄 $K, V$를 읽어 5번째 단어 "MUCH"를 생성하는 수치 연산.
8. **HBM 메모리 경제학 & 반도체 최적화 (Slide 37~44)**
   - 학습(Training) vs 추론(Serving) 메모리 점유 구조 차이
   - HBM 용량(Capacity) vs HBM 대역폭(Bandwidth) 2대 한계
   - **Roofline 모델** 및 modern LLM H/W 엔지니어링 3대 지침 (FlashAttention, PagedAttention, Quantization)
   - Multi-Head Attention & Positional Encoding 추후 세미나 과제 전개
