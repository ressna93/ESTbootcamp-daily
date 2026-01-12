# 2026년 01월 12일 프론트엔드 개발자 부트캠프 43일차

## 1교시 (09:00~10:00)

### React 학습 시작

- 교재 클론: https://github.com/KDT-10/react-lecture-10
- 라이브러리 vs 프레임워크 비교
- React, Vue, Angular 비교 분석

### Vite로 프로젝트 생성

```bash
npm create vite@latest my-vue-app -- --template vue
```

## 2교시 (10:00~11:00)

### 개발 환경 구성

- 터미널 관리자 권한 실행 (Windows 실행정책 오류 해결)
- Vite 설치 및 프로젝트 구성
- 빌드, 개발서버, Prettier/ESLint 설정
- TailwindCSS 설정

## 3교시 (11:00~12:00)

### React Props와 State

- **Props**: 부모 → 자식 컴포넌트로 데이터 전달
- **State**: 컴포넌트 내부에서 관리하는 상태

## 4교시 (13:00~14:00)

### State와 Props 동작원리

- 상태 변경 시 리렌더링 발생
- 단방향 데이터 흐름

## 5교시 (14:00~15:00)

### Props Drilling 문제점

- 중간 컴포넌트들이 불필요하게 props 전달
- 코드 가독성 저하, 유지보수 어려움

## 6교시 (15:00~16:00)

### Context API

- Props Drilling 해결책
- 전역 상태 관리 가능

## 7교시 (16:00~17:00)

### React Hooks

- **Hook 개념**: 함수형 컴포넌트에서 상태와 생명주기 사용
- **useState**: 컴포넌트 상태 관리
- React 19 업데이트 내용 확인

## 8교시 (17:00~18:00)

### useState vs useRef

| 구분 | useState | useRef |
|------|----------|--------|
| 리렌더링 | O | X |
| 용도 | UI 상태 관리 | DOM 참조, 값 유지 |

---

## 오늘의 핵심

1. React 개발 환경 구성 (Vite)
2. Props, State 개념 이해
3. Props Drilling → Context API로 해결
4. Hooks (useState, useRef) 학습
