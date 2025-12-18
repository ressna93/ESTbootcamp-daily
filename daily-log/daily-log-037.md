# TIL - Day 37 (2025.12.18)

프론트엔드 개발자 부트캠프 37일차
**주제**: JavaScript 비동기 처리 - 콜백, Promise, async/await

---

## 학습 내용

### 1교시 (09:00~10:00) - 함수형 프로그래밍 기초

#### JavaScript에서 함수는 일급 객체

- 함수를 변수에 할당 가능
- 함수를 인자로 전달 가능
- 함수를 반환값으로 사용 가능

```javascript
// 함수를 변수에 할당
const greet = function (name) {
  return `Hello, ${name}!`;
};

// 함수를 인자로 전달
function executeFunction(fn, value) {
  return fn(value);
}

console.log(executeFunction(greet, "World")); // Hello, World!
```

---

### 2~3교시 (10:00~12:00) - 콜백 지옥과 소프트웨어 계층 구조

#### 콜백 지옥(Callback Hell)이란?

비동기 작업을 순차적으로 처리하기 위해 콜백 함수를 중첩시키면서 발생하는 가독성 문제

```javascript
// 콜백 지옥 예시
getData(function (a) {
  getMoreData(a, function (b) {
    getMoreData(b, function (c) {
      getMoreData(c, function (d) {
        getMoreData(d, function (e) {
          console.log("최종 결과:", e);
        });
      });
    });
  });
});
```

#### 소프트웨어 스택 계층구조

**계층 구조 (아래에서 위로)**

```
┌─────────────────────────┐
│   응용 프로그램 계층     │  ← 추상화 (사용자 친화적)
├─────────────────────────┤
│   프레임워크/라이브러리  │
├─────────────────────────┤
│   프로그래밍 언어        │
├─────────────────────────┤
│   운영체제              │
├─────────────────────────┤
│   하드웨어              │  ← 구체화 (기계 친화적)
└─────────────────────────┘
```

- **구체화(Concretization)**: 하위 계층으로 갈수록 하드웨어에 가까운 구체적인 구현
- **추상화(Abstraction)**: 상위 계층으로 갈수록 복잡한 세부사항을 숨기고 단순한 인터페이스 제공

---

### 4교시 (13:00~14:00) - 콜백 패턴의 한계와 Promise

#### 콜백 패턴의 3가지 단점

1. **콜백 중첩에 따른 가독성 저하**

   - 들여쓰기가 깊어져 코드 파악이 어려움
   - "Pyramid of Doom" 발생

2. **후속 처리의 어려움**
   - 비동기 처리 결과를 상위 스코프 변수에 할당 불가
   - 콜백 함수 내부에서만 처리해야 함

```javascript
let result;

getData(function (data) {
  result = data; // 비동기이므로 외부에서 result 사용 시 undefined
});

console.log(result); // undefined (비동기 완료 전 실행)
```

3. **에러 처리 부족**
   - try-catch로 비동기 에러를 잡을 수 없음
   - 각 콜백마다 에러 처리 코드 필요

#### Promise의 개요

Promise는 비동기 작업의 최종 완료 또는 실패를 나타내는 객체

```javascript
const promise = new Promise((resolve, reject) => {
  // 비동기 작업
  const success = true;

  if (success) {
    resolve("성공 데이터");
  } else {
    reject("에러 메시지");
  }
});

promise
  .then((data) => console.log(data))
  .catch((error) => console.error(error));
```

---

### 5교시 (14:00~15:00) - Promise의 3가지 상태

#### Promise States

1. **Pending (대기)**: 약속 이행 전 상태

   - 비동기 처리가 아직 완료되지 않은 상태

2. **Fulfilled (이행)**: 약속이 이행됨

   - 비동기 요청 처리 결과가 성공적으로 응답됨
   - `resolve()` 호출됨

3. **Rejected (거부)**: 약속 이행 실패
   - 요청 처리 실패 및 에러 메시지 반환
   - `reject()` 호출됨

```javascript
// Promise 상태 변화 예시
const myPromise = new Promise((resolve, reject) => {
  console.log("상태: Pending");

  setTimeout(() => {
    const random = Math.random();

    if (random > 0.5) {
      resolve("성공!"); // 상태: Fulfilled
    } else {
      reject("실패!"); // 상태: Rejected
    }
  }, 1000);
});

myPromise
  .then((result) => console.log("Fulfilled:", result))
  .catch((error) => console.log("Rejected:", error))
  .finally(() => console.log("완료 (settled)"));
```

---

### 6교시 (15:00~16:00) - Promise 체이닝과 async/await

#### Promise 체이닝으로 순차 비동기 처리

```javascript
// 2단계 비동기 요청 체인
function getUser(userId) {
  return fetch(`/api/users/${userId}`).then((response) => response.json());
}

function getPosts(userId) {
  return fetch(`/api/users/${userId}/posts`).then((response) =>
    response.json()
  );
}

// Promise 체이닝
getUser(1)
  .then((user) => {
    console.log("사용자:", user);
    return getPosts(user.id);
  })
  .then((posts) => {
    console.log("게시글:", posts);
  })
  .catch((error) => {
    console.error("에러 발생:", error);
  });
```

#### async/await로 가독성 높이기

```javascript
// async/await 버전 - 동기 코드처럼 읽힘
async function getUserWithPosts(userId) {
  try {
    const user = await getUser(userId);
    console.log("사용자:", user);

    const posts = await getPosts(user.id);
    console.log("게시글:", posts);

    return { user, posts };
  } catch (error) {
    console.error("에러 발생:", error);
  }
}

getUserWithPosts(1);
```

#### 중요 개념

> **Q: async 테두리는 비동기적이지만, await 내부 내용은 동기적으로 동작하나요?**
>
> **A**: 정확합니다!
>
> - `async` 함수 자체는 **비동기적으로 실행**됩니다 (Promise 반환)
> - `await` 키워드는 해당 Promise가 완료될 때까지 **함수 실행을 일시 중지**합니다
> - `await` 이후의 코드는 Promise가 resolve된 후 **순차적으로** 실행됩니다
> - 하지만 다른 코드(함수 외부)는 블로킹되지 않고 계속 실행됩니다

```javascript
console.log("1. 시작");

async function example() {
  console.log("2. async 함수 시작");

  const result = await delay(1000); // 여기서 1초 대기
  console.log("4. await 완료:", result);

  return "done";
}

example();
console.log("3. async 함수 호출 직후 (블로킹 안됨)");

// 출력 순서: 1 → 2 → 3 → 4
```

---

### 7~8교시 (16:00~18:00) - 실전 프로젝트 리팩토링

#### 게시글 조회 후 작성자 정보 가져오기

**패턴 1: 유틸 함수 get() 활용**

```javascript
// utils.js
export async function get(url) {
  const response = await fetch(url);
  if (!response.ok) {
    throw new Error(`HTTP error! status: ${response.status}`);
  }
  return response.json();
}

// appV5.js
import { get } from "./utils.js";

async function getPostWithAuthor(postId) {
  try {
    // 1단계: 게시글 조회
    const post = await get(`/posts/${postId}`);
    console.log("게시글:", post);

    // 2단계: 작성자 조회
    const author = await get(`/users/${post.userId}`);
    console.log("작성자:", author);

    return { post, author };
  } catch (error) {
    console.error("에러:", error.message);
  }
}
```

**패턴 2: 단일 함수에서 fetch 직접 호출**

```javascript
// appV5.js
async function findUser(postId) {
  try {
    // 1) 게시글 조회
    const postResponse = await fetch(`/posts/${postId}`);
    const post = await postResponse.json();

    // 2) 작성자 조회
    const userResponse = await fetch(`/users/${post.userId}`);
    const user = await userResponse.json();

    return { post, user };
  } catch (error) {
    console.error("사용자 조회 실패:", error);
    throw error;
  }
}
```

#### 파일 분리 구조

```
project/
├── serverV5.js      # 서버 코드 (API 엔드포인트)
├── appV5.js         # 클라이언트 메인 로직
└── utils/
    ├── http.js      # HTTP 요청 유틸 함수
    └── helper.js    # 기타 헬퍼 함수
```

---

## 내일 실습 프로젝트 아이디어

### 1. 검색 컴포넌트

- 연관 검색어 자동완성
- 입력 텍스트 하이라이팅
- 디바운싱(debouncing) 적용

### 2. 페이지네이션

- 페이지 번호 기반 데이터 로딩
- 이전/다음 버튼 구현
- 현재 페이지 표시

### 3. 탭 전환

- 탭 클릭 시 컨텐츠 변경
- 상태 관리
- URL 파라미터 연동

### 4. 무한 스크롤

- Intersection Observer API 활용
- 스크롤 이벤트 최적화
- 로딩 상태 표시

---

## 핵심 정리

### 비동기 처리 발전 과정

```javascript
// 1. 콜백 (Callback)
getData(function (result) {
  // 중첩...
});

// 2. Promise
getData()
  .then((result) => {})
  .catch((error) => {});

// 3. async/await (권장)
async function example() {
  const result = await getData();
}
```

### 각 방식의 장단점

| 방식            | 장점                            | 단점                        |
| --------------- | ------------------------------- | --------------------------- |
| **콜백**        | 간단한 비동기 처리 가능         | 콜백 지옥, 에러 처리 어려움 |
| **Promise**     | 체이닝 가능, 에러 처리 개선     | 여전히 `.then()` 중첩 가능  |
| **async/await** | 동기 코드처럼 작성, 가독성 최고 | 에러 처리 시 try-catch 필요 |

---

## 오늘의 질문

**Q: async 테두리(비동기적이지만) await 내부 내용(에서는 동기적으로) 일까요?**

**A**:

- `async` 함수는 **항상 Promise를 반환**하며 비동기적으로 동작
- `await`는 Promise가 settled될 때까지 **해당 함수의 실행만 일시 중지**
- await 이후 코드는 순차적으로 실행되지만, 다른 코드는 블로킹되지 않음
- 즉, **함수 내부는 동기적으로 보이지만, 함수 자체는 비동기적**으로 동작

```javascript
async function foo() {
  console.log("1");
  await delay(100);
  console.log("3"); // await 완료 후 실행
}

foo();
console.log("2"); // foo()가 블로킹하지 않음

// 출력: 1 → 2 → 3
```

---

## 참고 자료

- [MDN - Promise](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise)
- [MDN - async function](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/async_function)
- [MDN - await](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/await)
- [JavaScript.info - async/await](https://ko.javascript.info/async-await)

---

## 오늘의 체크리스트

- [x] 콜백 지옥 개념 이해
- [x] Promise 3가지 상태 학습
- [x] async/await 문법 실습
- [x] 비동기 요청 체이닝 구현
- [x] 코드 리팩토링 및 파일 분리
- [x] 내일 프로젝트 아이디어 구체화

---

**Today I Learned**: 비동기 처리는 콜백 → Promise → async/await로 발전하며 가독성과 유지보수성이 크게 개선되었다. 특히 async/await는 동기 코드처럼 작성할 수 있어 복잡한 비동기 로직도 쉽게 이해할 수 있다.
