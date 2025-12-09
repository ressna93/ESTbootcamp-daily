# 2025년 12월 09일 — 프론트엔드 개발자 부트캠프 30일차 TIL

1교시 (09:00 ~ 10:00)
동기 / 비동기 / Promise 복습

JS는 싱글 스레드 기반에서 동작
작업을 처리하는 방식

동기(Sync): 이전 작업이 끝나야 다음 작업 시작

비동기(Async): 백그라운드에서 작업 처리 후 콜백 실행

대표 비동기 처리 방식
콜백(callback)

Promise
async/await (Promise 기반 문법적 설탕)

2교시 (10:00 ~ 11:00)
정규 표현식 기본
정규표현식 생성 방식
리터럴 방식 (일반적으로 사용)

```js
const regex = /hello/;
```

생성자 방식 (동적으로 패턴 생성할 때)

```js
const pattern = "hello";
const regex = new RegExp(pattern);
```

핵심 문법

1. 시작(^)과 끝($)

   > /^hello/ - hello로 시작
   > /world$/ - world로 끝남

2. 수량자(Quantifiers)

   > 표현 -----------의미
   > a\* ------------0회 이상 반복
   > a+ ------------1회 이상 반복
   > a? ------------0 또는 1회
   > a{3} ----------정확히 3회
   > a{2,4} --------2~4회
   > a{2,} ----------2회 이상

3. 문자 클래스(Character Classes)
   패턴------------- 의미
   [abc] ------------a,b,c 중 하나
   [0-9] -------------숫자
   [a-z] -------------소문자
   \d ---------------숫자
   \w ---------------문자 + 숫자 + 밑줄
   \s ---------------공백

4. 그룹 & 범위

```js
/(abc)+/
/(hello|world)/
```

5. 캡처링(Capturing)

```js
const result = "2025-12-09".match(/(\d{4})-(\d{2})-(\d{2})/);
```

6. 전방 탐색(Lookahead)

```js
/\d+(?=원)/; // 뒤에 "원"이 따라오는 숫자
```

실용 예제
이메일 검사

```js
/^[a-zA-Z0-9._-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/;
```

전화번호

```js
/^010-?\d{4}-?\d{4}$/;
```

HTML 태그 제거

```js
html.replace(/<[^>]*>/g, "");
```

3교시 (11:00 ~ 12:00)
최적화 (Optimization)

1. 최적화란?
   더 빠르고 효율적이며, 메모리 사용을 줄이는 프로그래밍 기법

“Make it work → Make it right → Make it fast”

2. 성능 측정 척도

시간(Time): 로딩·계산·반응 속도
메모리(Memory): 불필요한 데이터 차지 여부

3. 시간 최적화
   3.1 초기 구동시간
   파일 용량 최소화
   코드 분할, 레이지 로딩
   이미지 최적화(WebP, AVIF)

3.2 계산 시간 최적화
O(n) 알고리즘 사용
중첩 반복문(O(n²)) 지양

3.3 반응 시간 최적화 (DOM 중심)
DOM 조작 최소화
DocumentFragment 사용

### 디바운싱(Debounce)

마지막 입력 이후 일정 시간 뒤 실행

```js
function debounce(func, delay) {
  let timeoutId;
  return function (...args) {
    clearTimeout(timeoutId);
    timeoutId = setTimeout(() => func.apply(this, args), delay);
  };
}
```

### 스로틀(Throttle)

일정 주기마다 한 번만 실행

```js
function throttle(func, delay) {
  let last = 0;
  return function (...args) {
    const now = Date.now();
    if (now - last >= delay) {
      last = now;
      func.apply(this, args);
    }
  };
}
```

4교시 (13:00 ~ 14:00)

알고리즘 효율성
효율적: O(n)
비효율적: O(n²)
→ 중첩 루프 줄이는 것이 핵심
DOM 성능 최적화(Reflow/Repaint)

비효율적 DOM 조작

```js
items.forEach((item) => {
  const li = document.createElement("li");
  list.appendChild(li); // 리플로우 반복
});
```

효율적 DOM 조작 — DocumentFragment

```js
const fragment = document.createDocumentFragment();

items.forEach((item) => {
  const li = document.createElement("li");
  fragment.appendChild(li);
});

list.appendChild(fragment); // 한 번의 리플로우
```

5교시 (14:00 ~ 15:00)

리플로우(Reflow)와 리페인트(Repaint)
Reflow(Layout)
레이아웃 관련 속성이 변할 때 발생
비용이 가장 큼

## Repaint

단순 색상/배경 변화 등
Reflow보다 비용 낮음

DocumentFragment를 사용하는 이유

DOM에 직접 영향 X → 리플로우 발생 안 함
마지막에 한 번만 DOM에 삽입 → 최적화 극대화
강제 동기 레이아웃(Layout Thrashing) 방지

6교시 (15:00 ~ 16:00)
디바운스 & 스로틀 실습

메모리 누수 방지

1. 이벤트 리스너 제거

```js
button.addEventListener("click", handle);

button.removeEventListener("click", handle);
```

2. WeakMap 사용

객체가 참조를 잃으면 값도 자동 삭제 → 누수 방지

```js
const wm = new WeakMap();
let obj = { name: "test" };
wm.set(obj, 123);

obj = null; // 자동 GC → WeakMap 내부도 제거됨
```

7교시 (16:00 ~ 17:00)
효율적인 자료구조 선택
Object vs Map
비교 Object Map
키 타입 문자열만 모든 타입 가능
성능 느림 대량 데이터에 강함
순회 for...in for...of 가능
Array vs Set

배열: 중복 허용
Set: 중복 자동 제거
검색 속도: Set > Array
엄격 모드 (Strict Mode)
"use strict";

주요 기능
선언되지 않은 변수 사용 금지
읽기 전용 속성에 값 할당 금지
예약어 사용 금지
중복 매개변수 금지

8교시 (17:00 ~ 18:00)

- 개인 복습 시간
- 오늘 정리

정규표현식 기본 문법 및 실용 패턴 숙지
최적화(시간·메모리·DOM) 개념 완전 이해
리플로우/리페인트 비용 차이 학습
DocumentFragment를 통한 실무 성능 개선
디바운스 / 스로틀 패턴 완전히 익힘
자료구조 선택이 성능에 미치는 영향 체험
