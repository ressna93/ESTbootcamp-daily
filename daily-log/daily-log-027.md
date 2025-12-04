## 🔥 JavaScript 핵심 개념 요약

### 1. Destructuring (구조 분해 할당)

배열/객체에서 값을 쉽게 꺼내 변수로 저장

```js
const [a,b] = [1,2];
const {name, age} = {name:"영종", age:27};
필요한 값만 추출 가능
```

2. Rest (...)
   나머지를 묶어 배열/객체/인자로 받는 기능

```js
function sum(...nums){ return nums.reduce((a,b)=>a+b) }
 spread(펼침)과 반대 → rest는 묶음
```

3. Default Parameters
   값이 없을 때 기본값 자동 적용

```js
function hi(name = "Guest") {
  console.log(name);
}
```

4. Scope (스코프)
   변수를 사용할 수 있는 범위
   var=함수 스코프, let/const=블록 스코프

5. Callback Function
   다른 함수의 인자로 전달되어 나중에 실행

```js
setTimeout(()=>console.log("Done"),1000);
6. Hoisting
선언이 위로 끌어올려진 것처럼 동작
var는 선언만, let/const는 TDZ 존재
```

7. Recursion (재귀)
   함수가 자기 자신을 호출

```js
function countdown(n) {
  if (n <= 0) return;
  countdown(n - 1);
}
```

8. Closure (중요 ⭐)
   외부 함수의 변수를 기억하는 함수
   상태 유지 가능 (React 개념 연결 가능)

```js
function outer() {
  let n = 0;
  return () => console.log(++n);
}
```

9. Constructor Function
   객체 템플릿 생성 (new 사용)

```js
function User(name) {
  this.name = name;
}
new User("영종");
```

Map
Key-Value 저장 컬렉션 (Key 타입 자유, 순서 유지)

```js
const m=new Map();
m.set("name","영종");
m.get("name");
키에 객체/함수까지 가능
```

Set
중복 없는 value 컬렉션

```js
const s=new Set([1,1,2,3]);
[...s]; // [1,2,3]
배열 중복 제거 대표 활용
```

JSON (JavaScript Object Notation)
데이터 교환 표준 포맷
키와 문자열은 반드시 "큰따옴표"

```js
JSON.stringify(obj); // 객체 → 문자열
JSON.parse(str);     // 문자열 → 객체
통신/저장 시 필수
deep copy로 활용 가능(JSON 방식 한계 존재)
```

간단 요약

> Destructuring: 값 꺼내쓰기
> Rest: 나머지 묶기
> Default Params: 값 없으면 기본값
> Scope: 변수 사용 범위
> Callback: 나중에 실행할 함수
> Hoisting: 선언 끌어올림
> Recursion: 자기 호출
> Closure: 상태 기억
> Constructor: 객체 생성 템플릿
> Map: Key-Value, Key타입 자유
> Set: 중복 없는 데이터
> JSON: 데이터 교환 포맷 (stringify/parse)
