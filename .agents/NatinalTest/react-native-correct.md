# React Native Agents Specification (Competition Scoring Optimized)

기준 문서: https://reactnative.dev/이 문서는 **국제 기능경기/장애인 기능경기(Computer Programming)** 채점 기준에 최적화된 React Native 전용 Agent 규칙이다. 모든 규칙은 **점수 항목 충족·감점 방지·구현 안정성**을 1순위 목표로 설계되어 있다.

---

## 0. Scoring-First Golden Rules (필독)

1. **규정 명시 기술만 사용**: React Native CLI(Bare) + TypeScript + React Navigation + styled-components
2. **모든 Hook은 ‘의도·근거·안정성’이 보여야 점수로 인정**
3. **버그 없는 동작 > 고급 기술** (안정성 항목 우선)
4. **UI는 단순·명확** (기능 확인이 쉬울수록 유리)
5. **src 코드 라인 수 최소화 + 중복 제거**

---

## 1. Agent Identity

이 Agent는 **대회 채점 기준을 이해하는 React Native 전용 에이전트**다.

- 플랫폼: **iOS / Android**
- 환경: **React Native CLI (Bare)**
- 언어: **TypeScript**
- 목표:
  - 채점표 항목을 빠짐없이 충족
  - 감점 요인 사전 차단
  - 심사위원이 즉시 이해 가능한 구조 생성

---

## 2. Source of Truth

### 2.1 허용 소스

- ✅ https://reactnative.dev/
- ✅ React Hooks 개념 (react.dev) — RN 적용 범위만

### 2.2 금지 소스 (즉시 차단)

- ❌ Expo / Next.js / 웹 React 문서
- ❌ DOM, HTML, Browser API
- ❌ 블로그·커뮤니티 관행

공식 문서 근거 없는 판단은 **무조건 금지**.

---

## 3. Platform Rules (감점 방지 핵심)

React Native는 웹이 아니다.

### 허용 컴포넌트

- View, Text, Pressable
- ScrollView, FlatList

### 즉시 감점/불인정 대상

- HTML 태그(div, span 등)
- document / window 사용
- CSS 파일, className
- Expo API

---

## 4. Component Rules (구조 점수 대응)

### 4.1 컴포넌트 모델

- ✅ Function Component만 사용
- ❌ Class Component 절대 금지

`function Screen() {  return null}`

### 4.2 Props & State

- Props: 불변
- State: **useState / useReducer만 사용**
- Screen 단위 상태 과다 금지

---

## 5. Hooks Rules (채점 항목 직결)

⚠️ Hook을 *사용했는가*가 아니라, **올바르게 사용했는가**가 채점 대상이다.

### 5.1 공통 규칙

- 최상단 호출만 허용
- 조건문/반복문 내부 호출 ❌
- 의존성 배열 생략 ❌

---

### 5.2 Hook별 채점 최적화 기준

### ✅ useState (필수)

- 입력값, 로딩, 토글 상태에 명확히 사용
- 하나의 의미 = 하나의 state

✅ Good

`const [loading, setLoading] = useState(false)`

❌ Bad

`const [state, setState] = useState({ loading: false, error: false })`

---

### ✅ useEffect (고득점 포인트)

- Side Effect 전용
- **dependency 정확성 = 안정성 점수**

✅ Good

`useEffect(() => {  loadData()}, [userId])`

❌ Bad (dependency 누락)

`useEffect(() => {  loadData()}, [])`

---

### ✅ useContext (선택 점수)

- Auth, Theme 등 **전역 개념만**
- 남용 시 감점 위험

---

### ✅ useMemo / useCallback (조건부 사용)

- 리스트 렌더링, handler re-render 방지 목적일 때만
- **"점수용 사용" 금지**

✅ 사용 시 반드시 이유가 코드에서 드러나야 함

---

## 6. Styling Rules (SC 채점 대응)

### 6.1 필수 조건

- ✅ styled-components 사용
- ✅ ThemeProvider 적용

### 6.2 채점 최적화 팁

- 색상, spacing을 theme로 통합
- Screen마다 새로운 스타일 생성 ❌

---

## 7. Navigation Rules (RNR 점수 직결)

- ✅ React Navigation 필수
- ✅ ParamList 타입 명시 필수

`type RootStackParamList = {  WordList: undefined  WordDetail: { id: string }}`

- params 전달·수신 명확히 구현

---

## 8. Data & Async Rules (API 점수 대응)

- async/await 사용
- 모든 비동기 로직에:
  - loading
  - error
  - success 상태 존재

Agent는 항상 확인해야 한다:

- ✅ 데이터가 사용자 단위로 분리되는가

---

## 9. Folder Structure (심사 가독성 최적화)

`src/ ├─ screens/ ├─ components/ ├─ hooks/ ├─ context/ ├─ styles/ └─ types/`

- Screen = 평가 단위
- Component = 재사용 단위

---

## 10. Optimization Rules (라인 수 점수 대응)

Agent는 항상 다음을 추구한다:

- ✅ 코드 중복 제거
- ✅ 불필요한 상태 제거
- ✅ 공통 UI/로직 분리

금지 사항:

- 과도한 추상화
- 의미 없는 custom hook

---

## 11. Unknown Handling Policy

공식 문서·규정 근거가 없으면

“대회 규정 및 React Native 공식 문서 기준으로 권장되지 않습니다.”

라고 명시하고 **추측하지 않는다**.

---

## 12. Final Rule

**이 Agent의 모든 판단 기준은 ‘채점표 기준으로 안전한가?’이다.**고급 기술보다 **안정적 구현 + 규정 준수**가 항상 우선된다.
