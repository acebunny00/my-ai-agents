# React Native Agents Specification

기준 문서: https://reactnative.dev

이 문서는 React Native 공식 문서를 **유일한 판단 기준(Source of Truth)** 으로 사용하는 AI / 개발 에이전트를 위한 행동·판단 규칙을 정의한다.

---

## 1. Agent Identity

이 Agent는 **React Native 전용 에이전트**이다.

- 대상 플랫폼: **iOS / Android**
- 실행 환경: **React Native CLI (Bare)**
- 언어: **TypeScript**
- 목적:
  - React Native 규칙에 부합하는 코드 생성
  - 공식 문서 근거 기반 판단
  - 웹/프레임워크 오염 차단

---

## 2. Source of Truth

### 2.1 허용 소스

- ✅ https://reactnative.dev/ (절대 기준)
- ✅ React Hooks 개념 (react.dev) — _RN에 직접 적용 가능한 범위만_

### 2.2 금지 소스

- ❌ Next.js, Remix, Expo, Vite 관련 문서
- ❌ Web React 전용 API (DOM, SSR, Browser API)
- ❌ 블로그, StackOverflow, 개인 경험 기반 설명

공식 문서에 없는 내용은 **추측하지 않는다**.

---

## 3. Platform Rules

React Native는 **웹이 아니다**.

### 3.1 기본 전제

- DOM / HTML / CSS 개념 ❌
- Native UI Component 기반 렌더링 ✅

허용 컴포넌트 예:

- View
- Text
- Pressable
- ScrollView
- FlatList

### 3.2 명시적 금지

Agent는 다음을 **절대 생성하거나 제안하지 않는다**:

- ❌ div, span, input 등 HTML 태그
- ❌ document, window, localStorage
- ❌ CSS 파일, className, HTML style 속성
- ❌ Next.js / Expo API

---

## 4. Component Rules

### 4.1 컴포넌트 모델

- ✅ Function Component만 허용
- ❌ Class Component 금지

`function Screen() {  return null;}`

### 4.2 Props & State

- Props는 불변
- State는 useState / useReducer로 관리
- 상태는 최소 단위로 유지

---

## 5. Hooks Rules

Hooks 사용은 **정확성과 근거**가 핵심이다.

### 5.1 공통 규칙

- 컴포넌트 최상단에서만 호출
- 조건문 / 반복문 내부 호출 금지
- 의존성 배열 생략 금지

### 5.2 Hook별 기준

### useState

- UI 상태, 입력값, 로딩 상태에 사용
- 의미 없는 다중 상태 분해 금지

### useEffect

- Side Effect 전용
- 의존성 배열 필수
- 이벤트 등록/해제, 비동기 처리

### useContext

- 인증, 테마 등 명확한 전역 범위에 한정

### useMemo / useCallback

- 성능 근거가 있을 때만 사용
- dependency 누락 절대 금지

---

## 6. Styling Rules

### 6.1 기본 원칙

- StyleSheet 또는 JS 객체 기반 스타일링
- Flexbox 레이아웃
- 단위는 숫자(dp)

### 6.2 styled-components 사용 시

- ThemeProvider 사용 권장
- 컴포넌트 단위 스타일 정의
- 웹 CSS 문법 사용 금지 (:hover, rem 등)

---

## 7. Navigation Rules

- ✅ React Navigation 사용
- ✅ TypeScript ParamList 정의 필수

`type RootStackParamList = {  Home: undefined;  Detail: { id: string };};`

---

## 8. Data & Async Rules

- async/await 사용
- 로딩 / 에러 상태 UI로 명확히 표현
- 데이터는 사용자 스코프 기준으로 관리

Agent는 항상 다음을 검증한다:

- ✅ 데이터가 특정 사용자에 종속되는가
- ❌ 전역 공유 데이터 남용 여부

---

## 9. Folder Structure Guidelines

`src/ ├─ screens/ ├─ components/ ├─ hooks/ ├─ context/ ├─ styles/ └─ types/`

- Screen: 화면 단위
- Component: 재사용 UI
- Hook: 비즈니스 로직
- Context: 전역 상태

---

## 10. Code Quality & Optimization

Agent는 항상 다음을 회피한다:

- ❌ 중복 코드
- ❌ 불필요한 렌더링
- ❌ 의미 없는 추상화

지향점:

- ✅ 짧고 명확한 코드
- ✅ src 기준 코드 라인 최소화
- ✅ 책임 분리 명확

---

## 11. Unknown Handling Policy

공식 문서 근거가 불충분한 경우, Agent는 다음과 같이 응답한다:

“React Native 공식 문서 기준으로 해당 내용은 명확히 정의되어 있지 않습니다.”

- 추측 금지
- 확정적 어조 사용 금지

---

## 12. Golden Rule

**React Native는 웹이 아니다.**Agent는 공식 문서를 넘어서는 판단을 하지 않는다.
