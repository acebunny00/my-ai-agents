# agents.md

<!--
International Competition – Canonical Agent Guideline
Evaluation‑Friendly MAX + Perfectionist Version (FINAL)
This file is the single source of truth for development, evaluation, and submission.
-->

> ✅ 목적: **국제대회 기준에서 ‘정확히 동작하고, 읽기 쉬우며, 심사에 최적화된’ 결과물 완성**  > ✅ 범위: 프로젝트 생성 → 기능 완성 → 코드/구조 정제 → 심사 최적화 → 제출  > ✅ 전략: Phase 1(안정적 완성) → Phase 2(코드 품질) → Phase 3(심사 친화성)

---

## 0. Mandatory Usage Declaration

본 프로젝트에서 이루어지는 모든 판단, 구현, 리팩토링, 문서화는 이 `agents.md`를 유일한 기준으로 한다.

- 정의된 Phase, 체크리스트, 허용 범위를 벗어나지 않는다.
- “더 좋아 보이는 구현”보다 “평가 기준에 부합하는 구현”을 우선한다.

---

## 1. Authoritative References

기술적 판단의 최종 기준은 아래 공식 문서이다.

- React Native: https://reactnative.dev/docs/getting-started
- TypeScript: https://www.typescriptlang.org/docs/
- React Navigation: https://reactnavigation.org/docs/getting-started
- styled-components: https://styled-components.com/docs
- AWS Amplify: https://docs.amplify.aws/
- Amplify Auth: https://docs.amplify.aws/react/build-a-backend/auth/
- Amplify GraphQL: https://docs.amplify.aws/react/build-a-backend/graphqlapi/
- GraphQL Spec: https://spec.graphql.org/

Rule:
- 공식 레퍼런스와 AI 제안이 충돌하면 **공식 문서 우선**

---

## 2. Fixed Environment Assumptions

- React Native + TypeScript (Expo)
- AWS Amplify (Auth + GraphQL)
- 외부 API 사용 금지
- 모바일 어휘 암기 앱

---

## 3. Project Bootstrap

```bash
npx create-expo-app vocab-app --template expo-template-blank-typescript
cd vocab-app
npm install @react-navigation/native @react-navigation/native-stack             react-native-screens react-native-safe-area-context             styled-components aws-amplify
npm start
```

---

## 4. Amplify Bootstrap

```bash
amplify init
amplify add auth
amplify push
amplify add api
amplify push
```

---

## 5. Result-Oriented Checklist (Phase 1 – Baseline)

### Authentication
- [ ] Sign Up
- [ ] Sign In
- [ ] Sign Out
- [ ] Session 유지

### Data & CRUD
- [ ] Word(id, userId, term, meaning)
- [ ] Create / Read / Update / Delete
- [ ] userId 기반 데이터 분리

### Stability
- [ ] Loading 처리
- [ ] Error 처리 (Crash 없음)

✅ 완료 시 Phase 1 종료

---

## 6. Phase Strategy

### Phase 1 – Baseline Completion
- 요구사항 및 채점 기준 100% 충족
- 감점 요소 0

### Phase 2 – Code & Structure Refinement
- 가독성, 책임 분리, 중복 제거만 허용
- 기능 변경 금지

### Phase 3 – Evaluation Optimization
- 심사위원이 빠르게 이해할 수 있도록 문서·의도·동선 최적화

---

## 7. Requirement Traceability Rule

- 모든 Screen / Hook / 핵심 로직은 충족하는 요구사항을 주석으로 명시한다.

---

## 8. Assumption Disclosure

- 네트워크는 간헐적으로 불안정할 수 있음
- 데이터 규모는 소규모~중간 규모를 가정
- 안정성과 정확성을 최우선으로 함

---

## 9. Graceful Degradation Rule

- 네트워크/서버 오류 시 앱은 중단되지 않는다.
- 사용자에게 명확한 상태 메시지를 제공한다.

---

## 10. Commenting Policy (Why‑First)

- 주석은 **무엇을 하는지**가 아니라 **왜 그렇게 했는지**를 설명한다.

---

## 11. Evaluation Mode Guidance

- 기능 평가: Section 5
- 코드 품질 평가: Phase 2
- 설계 의도 평가: Sections 7–10

---

## 12. Explicit Non‑Goals

- Offline‑first 아키텍처
- 고급 캐싱/동기화
- UI 애니메이션

---

## 13. Reproducibility Statement

본 프로젝트는 숨겨진 의존성 없이 재현 가능하도록 설계되었다.

---

## Final Declaration

✅ Phase 1은 통과를 보장하고  ✅ Phase 2는 실력을 보여주며  ✅ Phase 3는 심사를 유리하게 만든다.
