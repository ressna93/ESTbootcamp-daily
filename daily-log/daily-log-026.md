# 2025년 12월 03일 프론트엔드 개발자 부트캠프 26일차

## JavaScript 기초 다지기 — 핵심 문제 풀이 중심 TIL

---

## 오늘의 학습 목표

- JavaScript 객체(Object) 다루기
- 조건문과 반복문 기본기 → 실전 연습
- 함수(Function) 선언·표현식·화살표 함수 이해
- Spread Syntax(전개 구문) & 구조분해할당 활용

오늘은 문제 풀이 중심으로 진행되었기 때문에, 핵심 예제만 정리하고  
“문제 설명 + 코드 + 해석” 형태로 정리했습니다.

---

---

# 1교시 — Object 정적 메소드 핵심 정리

## 1) Object.keys / values / entries

```js
const user = { name: "Kim", age: 28 };

console.log(Object.keys(user));     // ["name", "age"]
console.log(Object.values(user));   // ["Kim", 28]
console.log(Object.entries(user));  // [["name", "Kim"], ["age", 28]]
해석:
객체를 배열처럼 다루고 싶을 때 사용합니다.
특히 entries()는 for...of와 함께 사용할 때 유용합니다.

2) Object.assign (얕은 복사)
js
코드 복사
const a = { x: 1 };
const b = { y: 2 };

const result = Object.assign({}, a, b);
console.log(result); // { x: 1, y: 2 }
해석:
여러 객체를 하나로 병합할 때 사용합니다. 새로운 객체가 생성되며 원본은 유지됩니다.

3) 속성 존재 여부 확인
js
코드 복사
const car = { brand: "BMW", year: 2020 };

console.log("brand" in car);        // true
console.log(car.hasOwnProperty("year")); // true
해석:

in 연산자: 프로토타입 체인까지 확인

hasOwnProperty: 객체가 직접 가진 속성만 확인

2교시 — 조건문 핵심 문제 풀이
문제 1) 기본 if 문 — 성인 여부 판별
js
코드 복사
const age = 20;

if (age >= 18) {
  console.log("성인입니다");
}
해석:
조건이 참일 때만 코드가 실행됩니다.

문제 2) if-else 문 — 짝수/홀수
js
코드 복사
const num = 7;

if (num % 2 === 0) {
  console.log("짝수");
} else {
  console.log("홀수");
}
해석:
조건이 참이 아닌 경우 else가 실행됩니다.

문제 3) if-else-if — 학점 계산
js
코드 복사
const score = 82;
let grade;

if (score >= 90) grade = "A";
else if (score >= 80) grade = "B";
else if (score >= 70) grade = "C";
else grade = "F";

console.log(grade);
해석:
여러 조건이 순서대로 평가되고 처음으로 true가 되는 조건이 실행됩니다.

문제 4) switch 문 — 요일
js
코드 복사
const day = 3;
let name;

switch (day) {
  case 1: name = "월요일"; break;
  case 2: name = "화요일"; break;
  case 3: name = "수요일"; break;
  default: name = "기타";
}

console.log(name);
해석:
값이 특정 경우에 맞는지 비교할 때 if보다 코드가 깔끔합니다.

3교시 — 반복문 핵심 문제 풀이
문제 1) 기본 for 문 — 1부터 10까지 출력
js
코드 복사
for (let i = 1; i <= 10; i++) {
  console.log(i);
}
해석:
초기값 → 조건 → 증가 순서로 반복합니다.

문제 2) for...of — 배열 값 순회
js
코드 복사
const colors = ["red", "green", "blue"];

for (const c of colors) {
  console.log(c);
}
해석:
배열의 요소를 직접 꺼내 사용하기 때문에 매우 직관적입니다.

문제 3) while 문 — 조건 기반 반복
js
코드 복사
let count = 3;

while (count > 0) {
  console.log(count);
  count--;
}
해석:
조건식이 true인 동안 반복됩니다.

문제 4) 중첩 for 문 — 구구단 (2단 예시)
js
코드 복사
for (let i = 1; i <= 9; i++) {
  console.log(`2 x ${i} = ${2 * i}`);
}
해석:
중첩 반복은 규칙적인 계산이나 2차원 배열 처리에 많이 사용됩니다.

4교시 — 함수(Function) 핵심 문제 풀이
문제 1) 함수 선언문
js
코드 복사
function add(a, b) {
  return a + b;
}

console.log(add(3, 5)); // 8
해석:
호이스팅되므로 선언 이전에도 사용 가능합니다.

문제 2) 함수 표현식
js
코드 복사
const multiply = function (x, y) {
  return x * y;
};

console.log(multiply(4, 2)); // 8
해석:
변수에 함수가 저장되며, 호이스팅되지 않습니다.

문제 3) 화살표 함수
js
코드 복사
const hello = (name) => `Hello, ${name}!`;

console.log(hello("Kim"));
해석:
간결한 문법과 this 바인딩 차이가 특징입니다.

문제 4) 기본 매개변수
js
코드 복사
function greet(name = "Guest") {
  return `Hello, ${name}`;
}

console.log(greet());       // Hello, Guest
console.log(greet("Kim"));  // Hello, Kim
해석:
값이 전달되지 않았을 때 기본값이 사용됩니다.

문제 5) IIFE (즉시 실행 함수)
js
코드 복사
(function () {
  console.log("즉시 실행됩니다!");
})();
해석:
정의 즉시 실행되며 스코프 오염을 방지하는 용도로도 사용됩니다.

5교시 — Spread Syntax(전개 구문)
문제 1) 배열 복사
js
코드 복사
const arr = [1, 2, 3];
const copy = [...arr];

console.log(copy);
해석:
불변성을 유지하고 싶을 때 사용합니다. (얕은 복사)

문제 2) 배열 합치기
js
코드 복사
const a = [1, 2];
const b = [3, 4];

const merged = [...a, ...b];
console.log(merged);
해석:
concat보다 직관적이고 가독성이 좋습니다.

문제 3) 객체 복사
js
코드 복사
const user = { name: "Kim", age: 28 };
const newUser = { ...user };

console.log(newUser);
해석:
객체도 펼쳐서 새로운 객체를 만들 수 있습니다.

6교시 — 구조분해할당(Destructuring)
문제 1) 배열 구조 분해
js
코드 복사
const nums = [10, 20, 30];

const [a, b] = nums;

console.log(a, b); // 10 20
해석:
배열의 값을 간단하게 변수로 꺼낼 수 있습니다.

문제 2) 객체 구조 분해
js
코드 복사
const person = { name: "Kim", age: 29 };

const { name, age } = person;

console.log(name, age);
해석:
키 이름과 변수명이 일치해야 구조분해할당이 가능합니다.

문제 3) 변수 값 교환
js
코드 복사
let x = 1;
let y = 2;

[x, y] = [y, x];

console.log(x, y); // 2 1
해석:
임시 변수를 만들 필요 없이 교환할 수 있는 매우 유명한 패턴입니다.

오늘의 총정리
Object 메소드는 객체를 배열처럼 다룰 수 있게 해줍니다.

조건문은 특정 흐름 제어에 필수이며 반복문은 문제 해결의 기본기입니다.

함수는 선언 방식에 따라 동작 방식이 다르므로 구분이 중요합니다.

Spread는 배열·객체 조작에 매우 강력하며 구조분해할당은 필요한 값만 추출할 때 효과적입니다.

내일의 목표
함수 심화(클로저, 스코프) 이해

map / filter / reduce 확실히 정리

DOM 이벤트 핸들링 심화
```
