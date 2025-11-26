## 프론트엔드 부트캠프 — 개인 프로젝트 실습 기록

### (2025년 11월 25일 · 26일)

---

## 20일차 · 21일차

## 오늘의 목표

- 프로젝트 주요 섹션 UI 구성 (Hero · Card · Gallery · Subscribe)
- 모바일 우선(Mobile First) 반응형 구조 설계
- 모달 팝업 기능 구현 (Subscribe 클릭 시)
- Footer 데스크탑 레이아웃 정렬 문제 해결
- breakpoint(768px / 1024px / 1280px) 구간 이해 및 적용

---

## 진행한 작업 내용

### 1. Hero · Card · Gallery 섹션 구조 설계

- 전체 HTML 섹션 계층 구조 재정리
- Hero 텍스트 + 이미지 레이아웃 보완
- Card / Gallery 이미지 비율 조정
- Gallery 슬라이드를 위한 flex-sliding 기반 구조 설계

---

### 2. Subscribe Section UI 구현

- 모바일 우선 레이아웃으로 컴포넌트 구성
- 입력창 + 버튼 통합 UI 구성
- 라운드, 그림자, 색상 등 디자인 가이드에 맞게 스타일 조정
- Cat 이미지 오버랩을 위해 `margin-top: -100px` 적용 ((중요))

---

### 3. 반응형 레이아웃 구축

- 3단계 breakpoint 작성:
  - 768px(태블릿), 1024px(데스크탑 중간), 1280px 이상(풀 데스크탑)
- 1280px 이상에서 Subscribe 섹션 가로 배치
- 1024px 기반으로 960px × 270px 레이아웃 재정비
- flex-direction, gap, max-width로 전체 비율 안정화

---

### 4. Subscribe Modal 구현

- hidden 클래스로 show/hide 기능 구현
- 배경 클릭 시 모달 닫히는 로직 추가
- 데스크탑에서 보기 좋도록 480 × 380px로 크기 확장
- 텍스트, 아이콘, 버튼 비율을 데스크탑 기준으로 재조정

---

### 5. Footer 레이아웃 설계 및 정렬 문제 해결

- 모바일: 로고 → SNS → 메뉴 순서의 세로 정렬
- 데스크탑:
  - 로고 왼쪽 배치
  - SNS 아이콘 오른쪽 정렬
  - 메뉴는 데스크탑에서 숨김 처리
- `.footer-inner` → position: relative
- `.footer-social` → position: absolute
- HTML 구조 수정 없이 정렬 문제 해결

---

### 6. Media Query 로 시도 했던 것

```css
@media (min-width: 768px) and (max-width: 1023px) - min-width + max-width 조합으로 화면크기 범위를 잡아 보았습니다. --- ## 배운 점 1. 반응형은 “레이아웃 구조 → 사이즈 조정” 순서가 핵심 - 구조를 먼저 잡고사이즈 변경하는 방식이 가장 안정적일 것 같습니다. 실제로 첫 틀 을 잘못 잡아서 수정을 많이 하엿습니다. 2. HTML 구조가 레이아웃 문제 해결의 핵심 - Footer 정렬 이슈처럼 HTML 구조 이해가 CSS보다 우선 (1번) - 억지 CSS보다 구조 기반 설계가 중요함 (1번) 3. 모달은 모바일과 데스크탑을 분리해서 스타일링해야 함 - 모바일 기본 크기 → 데스크탑에서 확장 - 데스크탑 스타일을 바로 적용하면 모바일이 깨짐 - media query 필수 - 모달 되게 재밌는 포인트 였습니다,
  실력과 시간이 부족해 응용은 하지 못하였지만 충분히 시도 해보일만한 요소가 있었습니다. --- ## 내일 목표 - 각 button에 hover 적용 - 데스크탑 spacing 더 정교하게 조정 - etc..;
```
