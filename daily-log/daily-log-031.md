# TIL - 2025.12.10 (프론트개발자 부트캠프 31일차)

## 오늘 배운 내용

### 1️ Nullish 병합 연산자 (??)

**핵심 개념**

- ES2020에서 추가된 문법으로, 첫 번째 정의된(defined) 값을 반환

**연산자와의 차이점**

- `||` (OR) 연산자: 첫 번째 truthy 값을 반환
- `??` (nullish coalescing) 연산자: 첫 번째 정의된 값을 반환 (null, undefined만 체크)

---

### 2️ 자바스크립트 에러 핸들링

**try...catch...finally 구문**

```javascript
try {
  // 에러가 발생할 수 있는 코드
} catch (e) {
  // 에러 발생 시 실행될 코드
} finally {
  // 에러 발생 여부와 관계없이 항상 실행
}
```

---

### 3️ JavaScript sort() 함수

**기본 동작 원리**

- `compareFunction`이 제공되지 않으면 요소를 문자열로 변환
- 유니코드 코드 포인트 순서로 비교

---

### 4 불변성을 통한 코드 신뢰

**const 키워드의 중요성**

1. 의도치 않은 재할당 방지 (버그 예방)
2. 코드의 의도를 명확하게 표현 (가독성 향상)

**불변성의 장점**

- **예측 가능성**: 변수가 변경될 염려가 없어 코드 이해가 쉬움
- **디버깅 용이성**: 값이 변하지 않아 버그 추적이 간단함
- **코드 신뢰도**: 다른 개발자도 안심하고 코드를 사용할 수 있음

---

### 5️ 자바스크립트 변수 유효 범위

**var의 특징**

- 함수 스코프 (Function Scope)
- 호이스팅으로 인한 문제 발생 가능

**let, const의 특징**

- 블록 스코프 (Block Scope)
- TDZ (Temporal Dead Zone)로 인해 var의 예상치 못한 동작 방지

**핵심 포인트**

> 모던 JavaScript에서는 let과 const 사용을 권장하며, var 사용은 지양

---

### 6️ 배열 복사 및 정렬

**원본 배열 수정 (피해야 할 방식)**

```javascript
arr.sort(); //  원본 배열이 변경됨
```

**스프레드 문법으로 복사 후 정렬**

```javascript
const sorted = [...arr].sort(); //  원본 보존
```

---

### 7️ 로컬 스토리지와 메모 관리

**로컬 스토리지 개요**

- 웹 브라우저에서 제공하는 클라이언트 측 저장소
- 사용자의 브라우저에 데이터를 영구적으로 저장

**기본 사용법**

```javascript
// 저장
localStorage.setItem("key", "value");

// 가져오기
localStorage.getItem("key");

// 삭제
localStorage.removeItem("key");

// 전체 삭제
localStorage.clear();
```

**객체 데이터 저장**

```javascript
const data = { name: "John", age: 30 };
localStorage.setItem("user", JSON.stringify(data));

const user = JSON.parse(localStorage.getItem("user"));
```

---

### 8️ 자바스크립트 참/거짓과 드모르간 법칙

**Truthy와 Falsy 값**

**주요 Falsy 값들**

- `false`
- `0`, `-0`, `0n`
- `''` (빈 문자열)
- `null`
- `undefined`
- `NaN`

  **주요 Truthy 값들**

- Falsy가 아닌 모든 값
- `'0'`, `'false'`, `[]`, `{}`, `function(){}`

**동등 비교(==) vs 일치 비교(===)**

- `==`: 타입 변환 후 비교
- `===`: 타입까지 엄격하게 비교 (권장)

**드모르간 법칙 (De Morgan's Laws)**

```javascript
!(A && B) === !A || !B;
!(A || B) === !A && !B;
```

---

### 9️ 자바스크립트 날짜와 시간 다루기

**Date 객체 생성**

```javascript
// 현재 날짜와 시간
const now = new Date();

// 특정 날짜로 생성
const date1 = new Date(2025, 11, 10); // 2025년 12월 10일 (월은 0부터 시작)

// 특정 날짜 및 시간
const date2 = new Date(2025, 11, 10, 14, 30, 0);
```

**날짜 정보 가져오기 (Getter)**

```javascript
const now = new Date();
now.getFullYear(); // 년
now.getMonth(); // 월 (0-11)
now.getDate(); // 일
now.getDay(); // 요일 (0:일요일 ~ 6:토요일)
now.getHours(); // 시
now.getMinutes(); // 분
now.getSeconds(); // 초
```

**날짜 포맷팅**

```javascript
function formatDate(date) {
  const year = date.getFullYear();
  const month = String(date.getMonth() + 1).padStart(2, "0");
  const day = String(date.getDate()).padStart(2, "0");
  return `${year}-${month}-${day}`;
}
```

**시간차 계산 (D-day)**

```javascript
const today = new Date();
const targetDate = new Date("2025-12-25");
const diffTime = targetDate - today;
const diffDays = Math.ceil(diffTime / (1000 * 60 * 60 * 24));
```

---

### 자바스크립트 NaN 이해하기

**NaN이란?**

- NaN (Not a Number)은 숫자가 아님을 나타내는 특별한 숫자 값
- 자기 자신과도 같지 않은 유일한 값

**NaN의 특이한 특성**

```javascript
NaN === NaN; // false (!)
```

**NaN이 발생하는 경우**

- 숫자로 변환할 수 없는 문자열을 파싱할 때
- 정의되지 않은 수학 연산 (예: 0/0)
- 유효하지 않은 수학 함수 결과

**NaN 확인 방법**

1. **전역 함수 isNaN()**

```javascript
isNaN("hello"); // true
isNaN("123"); // false
isNaN(undefined); // true (예상치 못한 결과)
```

- 문제점: 인수를 숫자로 강제 변환 후 확인
- "이 값을 숫자로 바꿀 수 없니?"에 가까운 질문

2. **Number.isNaN() (ES6+)** 권장

```javascript
Number.isNaN(NaN); // true
Number.isNaN("hello"); // false
Number.isNaN(undefined); // false
```

- 인수를 변환하지 않고 정확히 NaN인지만 확인
- "이 값이 정말로 NaN이라는 바로 그 값이니?"라는 정확한 질문

**결론**

> 최신 JavaScript 환경에서는 항상 `Number.isNaN()` 사용을 권장

---

### 1️⃣1️⃣ 자바스크립트 변수 타입 확인

**타입 확인의 중요성**

- JavaScript는 동적 타입 언어
- 런타임에 변수의 타입을 정확히 확인하는 것이 중요

**1. typeof 연산자**

```javascript
typeof "hello"; // 'string'
typeof 123; // 'number'
typeof true; // 'boolean'
typeof undefined; // 'undefined'
typeof Symbol(); // 'symbol'
typeof function () {}; // 'function'
```

**typeof의 함정**

```javascript
typeof null; // 'object' ⚠️ (버그)
typeof []; // 'object' ⚠️
typeof {}; // 'object'
```

**2. instanceof 연산자**

```javascript
[] instanceof
  Array(
    // true
    {}
  ) instanceof
  Object; // true
new Date() instanceof Date; // true
```

**instanceof의 한계**

- 원시 타입에는 사용할 수 없음

**3. Array.isArray() (ES5+)** 배열 확인 권장

```javascript
Array.isArray([]); // true
Array.isArray({}); // false
```

**4. Object.prototype.toString.call()** 가장 정확

```javascript
Object.prototype.toString.call([]); // '[object Array]'
Object.prototype.toString.call({}); // '[object Object]'
Object.prototype.toString.call(null); // '[object Null]'
Object.prototype.toString.call(undefined); // '[object Undefined]'
```

**결론 및 추천 방법**

- **원시 타입** 확인: `typeof`
- **배열** 확인: `Array.isArray()`
- **특정 객체 인스턴스** 확인: `instanceof`
- **모든 타입을 명확히 구분**: `Object.prototype.toString.call()`

---

### 1️2️ 좋은 주석 작성법: JSDoc

**JSDoc 개요**

- 자바스크립트 API 문서 생성기
- Visual Studio Code에 기본 탑재

**기본 JSDoc 문법**

```javascript
/**
 * 두 수를 더하는 함수
 * @param {number} a - 첫 번째 숫자
 * @param {number} b - 두 번째 숫자
 * @returns {number} 두 수의 합
 */
function add(a, b) {
  return a + b;
}
```

**타입 힌트 활용 (@ts-check)**

```javascript
// @ts-check

/**
 * @typedef {object} Product
 * @property {number} id - 상품의 고유 ID
 * @property {string} name - 상품 이름
 * @property {number} price - 상품 가격
 * @property {boolean} inStock - 재고 여부
 */

/**
 * @param {Product} product - 상품 객체
 * @param {number} quantity - 수량
 * @returns {number} 총 가격
 */
function calculateTotal(product, quantity) {
  return product.price * quantity;
}
```

**TODO 및 FIXME 주석**

```javascript
// TODO: 에러 핸들링 추가 필요
// FIXME: 성능 이슈 개선 필요
```

**실무 주석 작성 팁**

1. **WHY를 설명하세요**: WHAT이 아닌 WHY를 주석으로 작성
2. **복잡한 로직 설명**: 알고리즘이나 비즈니스 로직의 의도 명시
3. **외부 의존성 명시**: API, 라이브러리 의존성에 대한 설명
4. **성능 고려사항**: 성능에 영향을 주는 코드에 대한 설명

---

## 오늘의 핵심 키워드

`Nullish Coalescing` `Error Handling` `Immutability` `TDZ` `localStorage` `Truthy/Falsy` `Date` `NaN` `Type Checking` `JSDoc`

## 느낀 점

- `Number.isNaN()`과 `isNaN()`의 차이를 아주 조금이나 알게 되었다
- 불변성의 중요성을 다시 한번 느꼈고, `const`를 기본으로 사용하는 습관을 들여야겠다
- 그러나 `var` 에 대한 개념도 생각은 하고 있을 것

## 내일 예정

코딩 테스트 및 자바스크립트 코딩 연습
