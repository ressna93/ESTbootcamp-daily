      // 변수 변하는수 , 변하는 정보
      // var - 과거의 산물
      // const - 상수
      // let - 변수

      // 선언
      let nickName;
      const guestName = "게스트"; // 게스트라는 고정값
      const greeting = "님 안녕하세요!";
      // 초기화
      ninkName = "김영종";

      // 사용 (내용)
      console.log(nickName + greeting); // " + "              1
      console.log(nickName, greeting); // " , "                2
      console.log(`${nickName} ${greeting}`); // " , "        3
      console.log(`${nickName}님 안녕하세요`);

      // 1번   nickName이란 문자열의 김영종 (let)  nickName = 김영종 // 김영종 + greeting의 문자열내용(님 안녕하세요) 와 더한다 = 김영종 님 안녕하세요!

      // console.log 란?  console.log()는 JavaScript에서 값을 화면(콘솔)에 출력하는 명령어
      //  개발자가 코드가 잘 작동하는지 확인하고 디버깅(debugging)할 때 가장 많이 사용하는 도구임

      // 1. 기본 기능: 출력하기
      // console.log("Hello");

      // 2. 변수 값 확인할 때
      // let age = 25;
      // console.log(age);

      // 3. 여러 개 출력도 가능
      // console.log("나이:", age, "살");

      // 4. 코드 흐름 디버깅용
      // function add(a, b) {
      // console.log("함수 실행됨");
      //  return a + b;
      // }

      // add(3, 5);

      // 6. 기타 다양한 콘솔 기능
      // console.log()	일반 출력
      // console.error()	에러 메시지 출력
      // console.warn()	경고 메시지 출력
      // console.table()	테이블 형태로 보기 좋게 출력

# 1.문자열 선언 방법

> let text1 = " Hello";
> let text2 = 'JavaScript';
> let text3 = `Template literal``; 마지막 따옴표는 마크다운 특성상 아직 실력이 부족하여 1개 나오개끔 불가

- 큰 따옴표,작은 따옴표,백틱 모두 문자열
- 백틱(`)은 $(변수)를 넣는 템플릿 리터럴에서 자주사용

# 2.문자열 주요 속성 / 메소드

- ## **(1)** 문자열 길이 확인 ㅡ `length`

> "Hello".length; // 5

- ## \*\*(2) 인덱스로 문자 접근

  > const str = "Hello";
  > str[0]; // 'H'
  > str[4]; // 'o'

- ## \*\*(3) 문자열변환 (대문자/소문자)

  > "hello".toUpperCase(); // "HELLO"
  > "WORLD".toLowerCase(); // "world"

- ## \*\*(4) 문자열 검색

  > "JavaScript".includes("Java); // true
  > "JavaScript".indexOf("Script); // 4 \*(위치)

- ## \*\*(5)문자열 자르기 (slice)

  > "JavaScript".slice(0, 4); // "Java"

- ## \*\*(6)문자열 교체 (replace)

  > "Hello World".replace("World", "JavaScript");
  > // "Hello JavaScript"

- ## \*\*(7)문자열 분리(split) → 배열

  > "사과,바나나,포도".split(",");
  > // ["사과", "바나나", "포도"]

- ## \*\*(8)문자열 결합(join) → 문자열

  > ["a", "b", "c"].join("-");
  > // "a-b-c"

- ## \*\*(9)공백 제거(trim)

  > " hello ".trim(); // "hello"

- ## \*\*(10)문자열 패딩 (padStart, padEnd)

  > "5".padStart(3, "0"); // "005"
  > "5".padEnd(3, "\*"); // "5\*\*"

- ## \*\*(11)실전 예제 — 이메일 검증

  > const email = "test@gmail.com";
  > email.includes("@"); // true
  > email.includes("."); // true

- ## \*\*(12)실전 예제 — URL 파싱

  > const url = "https://example.com/page?id=10";
  > url.split("?");
  > // ["https://example.com/page", "id=10"]

### 내용정리

- 문자열은 텍스트 데이터를 다루는 기본 타입

- 길이는 .length

- 글자 접근은 str[index]

- 대소문자 변환 toUpperCase(), toLowerCase()

- 검색 includes(), 위치 indexOf()

- 자르기 slice()

- 바꾸기 replace()

- 분리 split() / 결합 join()

- 공백 제거 trim()

- 패딩 padStart() / padEnd()

- 이메일 검증 → "@","." 포함 여부 확인

- URL 파싱 → split()으로 구분

# JavaScript 숫자(Number)

1. 숫자 리터럴(Number Literal)

> let n1 = 10; // 정수
> let n2 = 3.14; // 실수
> let n3 = -5; // 음수

2. 특별한 숫자 값

- 값 의미
  > Infinity 무한대
  > -Infinity 음의 무한대
  > NaN 숫자가 아님(Not a Number)
  > 10 / 0; // Infinity
  > -"hello"; // NaN

3. Number 객체 (정적 메소드)
   > 문자열 → 숫자 변환
   > Number("123"); // 123
   > Number("3.14"); // 3.14
   > Number("abc"); // NaN

> NaN인지 체크 (가장 정확)
> Number.isNaN(value);

4. Number 인스턴스 메소드

> 소수점 자리수 제한
> (3.14159).toFixed(2); // "3.14"
> (3.14159).toPrecision(3); // "3.14"

> !!! 문자열로 반환되므로 숫자로 쓰려면 Number()로 다시 변환해야 함.

4.  Math 객체 — 수학 유틸리티
    > 반올림/올림/내림
    > Math.round(3.6); // 4
    > Math.ceil(3.1); // 4
    > Math.floor(3.9); // 3

> 최대/최소
> Math.max(1, 20, 3); // 20
> Math.min(1, 20, 3); // 1

> 거듭제곱 / 제곱근
> Math.pow(2, 3); // 8
> Math.sqrt(16); // 4

> 난수 (0 ~ 1 사이)
> Math.random(); // 예: 0.3271...

> 문제로 이해하는 Number
> 문제 1: 숫자 타입 확인
> typeof 123; // "number"
> typeof 3.14; // "number"

> 문제 2: 문자열을 숫자로 변환
> Number("10"); // 10
> parseInt("10px"); // 10
> parseFloat("3.14cm"); // 3.14

> 문제 3: NaN 체크
> Number.isNaN(NaN); // true
> Number.isNaN("hello"); // false

> 문제 4: 소수점 다루기
> let price = 3.14159;
> price.toFixed(2); // "3.14"

> 문제 5: 진법 변환
> (10).toString(2); // "1010" → 2진수
> (255).toString(16); // "ff" → 16진수

> 문제 6: 반올림 / 올림 / 내림
> Math.round(7.5); // 8
> Math.ceil(7.1); // 8
> Math.floor(7.9); // 7

> 문제 7: 최대/최소 찾기
> Math.max(10, 5, 20); // 20
> Math.min(10, 5, 20); // 5

> 문제 8: 거듭제곱 / 제곱근
> Math.pow(2, 4); // 16
> Math.sqrt(81); // 9

> 문제 9: 난수 생성
> Math.random() // 0~1
> Math.random() _ 10 // 0~10
> Math.floor(Math.random() _ 6) + 1; // 1~6 주사위

> 문제 10: 실전 가격 계산

!!!! 소수점 실수 오차를 방지하려면 곱해서 정수로 계산 후 나누기!

> let price = 19900;
> let count = 3;
> let total = price \* count; // 59700

> total.toLocaleString(); // "59,700" (3자리 콤마)

- # Number 파트 한눈요약

- 숫자는 정수/소수/Infinity/NaN 모두 포함

- 타입 확인: typeof

- 문자열 → 숫자: Number(), parseInt(), parseFloat()

- NaN 체크: Number.isNaN()

  -소수점 처리: toFixed()

- 진법 변환: toString(2), toString(16)

- Math 객체: 반올림, 난수, 최대/최소, 제곱 등

- 실무에서 필수: 가격 계산 + toLocaleString()

# JavaScript Boolean (불리언)

## 1. Boolean 값

### 정의

Boolean은 **참(true)** 또는 **거짓(false)** 두 가지 값만 가지는 원시 타입.

### 이유 / 왜 필요한가?

조건문(if), 반복문, 유효성 검사 등 **프로그램의 흐름을 제어하기 위한 핵심 타입**이기 때문.

---

## 2. 논리 연산자 (Logical Operators)

### 종류

| 연산자 | 의미         | 예시                  |
| ------ | ------------ | --------------------- | --------- | ---- | --- | ------------ |
| `&&`   | AND (그리고) | true && false → false |
| `      |              | `                     | OR (또는) | true |     | false → true |
| `!`    | NOT (부정)   | !true → false         |

### 이유

여러 조건을 연결하여 더 복잡한 논리를 만들기 위해 사용.

---

## 3. Truthy 와 Falsy

### 정의

Boolean이 아니어도 조건식에서 true처럼(truthy) 또는 false처럼(falsy) 동작하는 값들.

### Falsy 값 (6개)

- `false`
- `0`
- `""`
- `null`
- `undefined`
- `NaN`

### Truthy 값

Falsy 6개를 제외한 모든 값.

### 이유

입력값 체크, 유효성 검사에서 매우 자주 사용됨.

---

## 4. 단축 평가 (Short-circuit Evaluation)

### 정의

논리 연산자가 **결과가 확정되는 순간 평가를 멈추는 성질**.

- `A || B` → A가 truthy면 B는 실행되지 않음
- `A && B` → A가 falsy면 B는 실행되지 않음

### 이유

기본값 제공, 조건부 실행, 함수 실행 제어 등 실무에서 많이 쓰임.

---

# Boolean — 실습 문제로 이해하기

## 문제 1: Boolean 기본

```js
true;
false;
typeof true; // "boolean"
```

---

## 문제 2: 논리 AND (&&)

```js
true && true; // true
true && false; // false
```

---

## 문제 3: 논리 OR (||)

```js
true || false; // true
false || false; // false
```

---

## 문제 4: 논리 NOT (!)

```js
!true; // false
!false; // true
```

---

## 문제 5: Falsy 값들

```js
Boolean(0); // false
Boolean(""); // false
Boolean(undefined); // false
Boolean(null); // false
Boolean(NaN); // false
```

---

## 문제 6: Truthy 값들

```js
Boolean("hello"); // true
Boolean(123); // true
Boolean([]); // true
Boolean({}); // true
```

---

## 문제 7: 이중 부정 (!!)

```js
!!"hello"; // true
!!0; // false
```

---

## 문제 8: 단축 평가 - OR (||)

```js
let name = "";
let userName = name || "Guest";
```

---

## 문제 9: 단축 평가 - AND (&&)

```js
let isAdmin = true;
isAdmin && console.log("관리자 접근");
```

---

## 문제 10: 실전 예제 - 접근 권한 체크

```js
let isLogin = true;
let isAdmin = false;

if (isLogin && isAdmin) {
  console.log("관리자 페이지 입장");
} else {
  console.log("권한 없음");
}
```

---

## 문제 11: 실전 예제 - 입력 유효성 검증

```js
let input = "";

if (!input) {
  console.log("입력값이 비어 있습니다.");
}
```

---

# Boolean 한눈 요약

- true/false 두 가지 값만 가진 원시 타입
- 논리 연산자: `&&`, `||`, `!`
- Truthy/Falsy 자동 변환 존재
- 단축 평가로 기본값 제공 및 조건부 실행 가능
- 실무에서 입력값 검사, 권한 체크 등에 많이 사용

# JavaScript — undefined & null 정리

undefined와 null은 모두 **'값이 없음'**을 나타내지만  
의미, 발생 원인, 사용 목적이 서로 다르다.

---

## 1. undefined (정의 + 이유)

**정의:**

- 값이 *할당되지 않은 상태*를 의미한다.
- 변수가 선언만 되고 아직 어떤 값도 넣지 않은 경우 자동으로 부여되는 값이다.

**이유:**

- JS 엔진이 “아직 값이 정해지지 않았음”을 표시하기 위해 자동으로 사용하는 기본값이다.

---

## 2. null (정의 + 이유)

**정의:**

- “의도적으로 비워둔 값”, 즉 **개발자가 값이 없음을 명시적으로 표현**하기 위한 값이다.

**이유:**

- 아직 객체를 넣기 어렵거나 비어있다는 상태를 명확히 표시할 때 사용한다.  
  (ex: 나중에 데이터가 들어올 자리를 먼저 null로 선언)

---

## 3. undefined와 null의 비교

| 비교 요소 | undefined            | null                        |
| --------- | -------------------- | --------------------------- |
| 의미      | 값이 할당되지 않음   | 값이 없음을 명시적으로 지정 |
| 발생 방식 | JS 엔진이 자동 부여  | 개발자가 직접 대입          |
| 타입      | `"undefined"`        | `"object"` (역사적 버그)    |
| 사용 목적 | 초기화되지 않은 상태 | 의도적 초기값/초기화        |

---

## 문제 1: undefined 발생 상황 (정의 + 이유)

### 정의

undefined는 “JS 엔진이 값이 없다고 판단할 때 자동으로 부여되는 값”.

### 왜 이런 상황이 발생하는가?

값이 지정되지 않았거나 접근하려는 값이 존재하지 않음을 알리기 위해.

### ▶ 예시

```js
let a;          // 선언만 함 → undefined
console.log(a); // undefined

function f(x) {
  console.log(x); // 전달되지 않은 인수 → undefined
}
f();

const obj = {};
console.log(obj.age); // 존재하지 않는 프로퍼티 → undefined

문제 2: null 사용 상황 (정의 + 이유)

정의
개발자가 **명확하게 "비어 있음"**을 표현할 때 사용하는 값.

이유
초기 상태를 명시하거나, 나중에 값이 채워질 예정임을 나타내기 위함.

예시
let user = null;  // 현재는 로그인된 유저 없음 (빈 상태)

문제 3: typeof 차이 (정의 + 이유)

정의
undefined → 타입이 "undefined"
null → 타입이 "object" (JS의 오래된 설계 오류)

이유
초기 JavaScript 설계 당시의 버그가 유지되고 있음.

예시
console.log(typeof undefined); // "undefined"
console.log(typeof null);      // "object"

문제 4: 동등(==) vs 일치(===) 비교

정의
== → 타입 변환 후 비교 (느슨한 비교)
=== → 타입 비교까지 포함 (엄격한 비교)

이유
undefined 와 null 은 둘 다 “값 없음”으로 취급되므로
동등 비교에서는 같다.

예시
undefined == null   // true
undefined === null  // false

문제 5: null/undefined 체크 패턴 (정의 + 이유)

정의
둘 다 “값이 비어있음”을 나타내므로 자주 함께 체크한다.

이유
서로 구분이 필요 없는 경우가 많기 때문.

패턴 예시
if (value == null) {
  // null 또는 undefined 인 경우
}

문제 6: Falsy 값으로서의 동작

정의
undefined와 null은 모두 JavaScript에서 Falsy 값이다.

이유
조건문에서 “값이 없음”을 false 취급하도록 되어 있기 때문.

예시
if (!undefined) console.log("undefined는 falsy");
if (!null) console.log("null도 falsy");

문제 7: 기본값 설정 패턴 (정의 + 이유)

정의
값이 null/undefined이면 기본값을 설정하는 패턴.

이유
API 응답 값이 비어있거나, 옵션 설정시 기본값이 필요할 때 자주 사용함.

예시 1 — OR 사용
let name;
console.log(name || "기본 이름");  // "기본 이름"

예시 2 — Null 병합 연산자 (추천)
let age = 0;
console.log(age ?? 20);  // 0 (정상 값이므로 그대로 유지)

문제 8: 옵셔널 체이닝 (?.) (정의 + 이유)

정의
중첩된 객체를 안전하게 접근하도록 해주는 연산자.

이유
null 또는 undefined인 값을 접근하면 에러가 발생하므로,
체이닝 도중에 null/undefined가 나오면 자동으로 평가를 중단해 undefined를 반환.

예시
const user = { profile: null };
console.log(user.profile?.name); // undefined (에러 없이 작동)

요약

undefined: 값이 “할당되지 않은 상태”, JS 엔진이 자동 결정
null: 개발자가 “값 없음”을 의도적으로 표현
비교할 때 ==는 동일하게 취급, ===는 완전히 다른 값으로 취급
실제 개발에서는 null과 undefined를 적절하게 구분해 사용
```

# JavaScript Array (배열)

Array: 여러 개의 값을 **순서대로 저장**하는 **참조 타입(객체)**입니다.

---

## 1. 배열 생성

```js
let nums = [1, 2, 3];
let fruits = ["apple", "banana", "orange"];
let mixed = [1, "text", true];
let arr = new Array(5); // 비어있는 길이 5 배열

2. 배열의 주요 속성과 접근
let arr = ["a", "b", "c"];

arr.length;     // 3
arr[0];         // "a"
arr[2];         // "c"
arr[arr.length - 1]; // 마지막 요소


인덱스는 0부터 시작
length는 요소 개수를 의미

3. 배열을 직접 수정하는 메소드 (Mutator Methods)

원본 배열이 변경됨!

arr.push(4);     // 끝에 추가
arr.pop();       // 끝에서 제거
arr.unshift(0);  // 앞에 추가
arr.shift();     // 앞에서 제거

arr.splice(1, 2, "X");
// 1번 인덱스부터 2개 삭제 후 "X" 삽입

4. 새로운 배열을 반환하는 메소드 (Accessor / Iteration Methods)

원본 배열은 유지됨!

arr.slice(1, 3);           // 일부 추출
arr.map(x => x * 2);       // 값 변환
arr.filter(x => x > 10);   // 조건 필터링
arr.reduce((a, c) => a + c, 0); // 누적 계산


5. 탐색 메소드
arr.indexOf("apple");     // 위치
arr.includes("apple");    // 포함 여부
arr.find(x => x > 10);    // 첫 번째 요소 반환
arr.findIndex(x => x > 10); // 위치 반환

실습 문제
문제 1: 배열 생성과 접근
let colors = ["red", "green", "blue"];
colors[1]; // "green"
colors.length; // 3

문제 2: push, pop - 배열 끝 조작
let arr = [1, 2];
arr.push(3); // [1, 2, 3]
arr.pop();   // [1, 2]

문제 3: unshift, shift - 배열 앞 조작
let arr = [2, 3];
arr.unshift(1); // [1, 2, 3]
arr.shift();    // [2, 3]

문제 4: splice - 요소 삭제/추가/교체
let arr = ["a", "b", "c", "d"];
arr.splice(1, 2);           // ["a", "d"]
arr.splice(1, 0, "X");      // ["a", "X", "d"]
arr.splice(1, 1, "Y");      // ["a", "Y", "d"]

문제 5: slice - 배열 복사
let arr = [1, 2, 3, 4];
let copy = arr.slice(1, 3); // [2, 3]

문제 6: map - 배열 변환
let nums = [1, 2, 3];
nums.map(x => x * 2); // [2, 4, 6]

문제 7: filter - 배열 필터링
let nums = [1, 2, 3, 4, 5];
nums.filter(x => x > 3); // [4, 5]

문제 8: reduce - 배열 축약
let nums = [1, 2, 3];
nums.reduce((acc, cur) => acc + cur, 0); // 6

문제 9: find, findIndex - 요소 찾기
let users = [
  { id: 1, name: "Kim" },
  { id: 2, name: "Lee" }
];

users.find(u => u.id === 2);       // { id: 2, name: "Lee" }
users.findIndex(u => u.id === 2);  // 1

문제 10: sort - 배열 정렬
[3, 1, 4, 2].sort();     // [1, 2, 3, 4]
["b", "a", "c"].sort();  // ["a", "b", "c"]

// 숫자를 제대로 정렬하려면 콜백 필요
[10, 2, 5].sort((a, b) => a - b); // [2, 5, 10]

문제 11: 실전 예제 - 장바구니 관리
let cart = [];

cart.push({ name: "apple", price: 1000 });
cart.push({ name: "banana", price: 1500 });

cart = cart.filter(item => item.name !== "apple");

cart.reduce((total, item) => total + item.price, 0);
// 총 가격 계산
```
