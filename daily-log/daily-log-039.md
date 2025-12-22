# 2025년 12월 22일 프론트엔드 개발자 부트캠프 39일차

## 2025년 12월 19일 프론트엔드 개발자 부트캠프 38일차는 개인프로젝트 진행하였던 날이여서 추후 github 다른 레포지에 업로드 예정.

## 오늘의 학습 주제

- npm, 프로젝트, 패키지 개념
- 코드 리팩토링 (fetch, async/await)
- 환경변수로 key값 관리
- Cypress E2E 테스트

---

## 1. npm & 프로젝트 실행 방법

### 프로젝트의 두 가지 유형

#### 1) 직접 운영하는 웹 서비스

- 예시: Papago, Google Drive, Figma Web, Notion Web
- SaaS(Software as a Service) 형태
- 소스코드가 아닌 서비스 자체를 제공

#### 2) 자체 모듈(라이브러리)

- 예시: superagent, express
- 다른 프로젝트에서 사용할 수 있도록 패키징된 코드
- npm을 통해 설치하여 사용
- npm = Node Package Manager

### package.json 주요 항목

#### 1) scripts

```json
{
  "scripts": {
    "start": "node server.js",
    "dev": "nodemon server.js",
    "test": "jest"
  }
}
```

- 전 세계적으로 공통된 별칭 사용 (start, dev, test 등)
- `npm run start` 또는 `npm start` (일부 명령어는 run 생략 가능)
- 그 외 명령어는 `npm run [명령어]` 형태로 사용

#### 2) dependencies (의존성)

```json
{
  "dependencies": {
    "express": "^5.2.1",
    "superagent": "^10.2.3"
  }
}
```

- 프로젝트가 실행되기 위해 필요한 모듈 목록
- 배포 환경에서도 필요한 의존성

#### 3) devDependencies

```json
{
  "devDependencies": {
    "cypress": "^13.0.0"
  }
}
```

- 개발 환경에서만 필요한 의존성
- 예시: 테스팅 라이브러리 (Cypress, Jest 등)

### 회사 프로젝트 받아서 실행하는 방법

```bash
# 1. 프로젝트 클론
git clone [프로젝트 주소]

# 2. 프로젝트 디렉토리로 이동
cd [프로젝트명]

# 3. 의존성 설치
npm install

# 4. 서버 실행 (package.json의 scripts 확인)
npm run dev
# 또는
npm start
```

#### 실습 예제

https://github.com/anis6205/To-Do-Manager

```bash
git clone https://github.com/anis6205/To-Do-Manager
cd To-Do-Manager
npm install
npm run dev  # 5173 포트에서 실행
```

---

## 2. 코드 리팩토링

### 리팩토링이란?

- 코드의 기능은 그대로 유지하면서 코드의 구조와 가독성을 개선하는 작업
- 더 효율적이고 유지보수하기 좋은 코드로 변경

### XHR → fetch & async/await 리팩토링

#### Before (XHR 방식)

```javascript
function translateText(text) {
  return new Promise((resolve, reject) => {
    const xhr = new XMLHttpRequest();
    xhr.open("POST", "/api/translate");
    xhr.setRequestHeader("Content-Type", "application/json");

    xhr.onload = function () {
      if (xhr.status === 200) {
        resolve(JSON.parse(xhr.responseText));
      } else {
        reject(new Error("Translation failed"));
      }
    };

    xhr.onerror = function () {
      reject(new Error("Network error"));
    };

    xhr.send(JSON.stringify({ text }));
  });
}
```

#### After (fetch & async/await 방식)

```javascript
async function translateText(text) {
  try {
    const response = await fetch("/api/translate", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify({ text }),
    });

    if (!response.ok) {
      throw new Error("Translation failed");
    }

    return await response.json();
  } catch (error) {
    throw new Error("Network error");
  }
}
```

#### 장점

- 코드가 더 간결하고 가독성이 높아짐
- 에러 처리가 더 직관적 (try-catch)
- Promise 체이닝보다 더 동기적인 코드 스타일

---

## 3. key 관리 (환경변수)

### key가 노출되면 안 되는 이유

- API key가 노출되면 누구나 해당 서비스를 무단으로 사용 가능
- 비용 청구, 보안 문제 발생 가능
- Github 같은 공개 저장소에 절대 올리면 안 됨

### 문제 상황

- api.js 코드는 팀원들과 협업을 위해 Github에 올려야 함
- 하지만 key값은 절대 올리면 안 됨

### 해결 방법: 환경변수 (.env)

#### 1) .env 파일 생성

```
# .env
PAPAGO_CLIENT_ID=your_client_id_here
PAPAGO_CLIENT_SECRET=your_client_secret_here
```

#### 2) .gitignore에 추가

```
# .gitignore
.env
node_modules/
```

#### 3) 코드에서 환경변수 사용

```javascript
// Before
const CLIENT_ID = "abc123xyz"; // 하드코딩 (위험!)
const CLIENT_SECRET = "secret456";

// After
const CLIENT_ID = process.env.PAPAGO_CLIENT_ID;
const CLIENT_SECRET = process.env.PAPAGO_CLIENT_SECRET;
```

#### 4) 환경변수 로드 (dotenv 패키지)

```bash
npm install dotenv
```

```javascript
// server.js 또는 api.js 상단에
require("dotenv").config();
```

### 환경변수의 종류

#### 1) OS 환경변수

- 운영체제 수준에서 사용하는 환경변수
- 예시: PATH, HOME 등

#### 2) 프로그램 환경변수

- 특정 프로젝트에서만 사용하는 환경변수
- .env 파일로 관리

### key가 노출되는 구체적인 경우

1. **Github에 .env 파일을 푸시한 경우**

   - .gitignore에 추가하지 않고 커밋

2. **소스코드에 하드코딩한 경우**

   ```javascript
   const API_KEY = "abc123xyz"; // 위험!
   ```

3. **클라이언트 사이드 코드에 노출한 경우**
   - 브라우저에서 실행되는 JavaScript 코드에 key를 포함
   - 브라우저 개발자 도구로 누구나 확인 가능

### 추가 보안 방법: AWS KMS

- KMS (Key Management Service)
- 클라우드 기반 key 관리 서비스
- 더 강력한 보안이 필요한 경우 사용

---

## 4. E2E 테스트 (Cypress)

### E2E 테스트란?

- End to End 테스트
- End (개발자) → End (실제 사용자)
- 사용자의 실제 사용 시나리오를 자동으로 테스트
- 전체 애플리케이션이 제대로 동작하는지 검증

### 테스트 코드가 필요한 이유

1. **자동화된 검증**

   - 매번 수동으로 테스트하는 것은 피곤함
   - 변경사항이 있을 때마다 자동으로 테스트 가능

2. **회귀 버그 방지**

   - 새로운 기능 추가 시 기존 기능이 깨지지 않는지 확인

3. **신뢰성 증명**

   - 누군가에게 구현 사항을 증명할 때 테스트 실행 기록 제공

4. **개발자로서 최선의 노력**
   - 테스트 커버리지 100%라도 모든 버그를 잡을 수는 없음
   - 하지만 개발자가 할 수 있는 최선

### 테스트 피라미드

```
        /\
       /E2E\        ← 적은 수의 E2E 테스트
      /------\
     /컴포넌트\      ← 중간 수의 컴포넌트 테스트
    /----------\
   /   Unit     \   ← 많은 수의 단위 테스트
  /--------------\
```

- **Unit (단위 테스트)**: 개별 함수, 메서드 테스트 (가장 많이)
- **Component (컴포넌트 테스트)**: React 컴포넌트 테스트 (중간)
- **E2E (통합 테스트)**: 전체 사용자 시나리오 테스트 (적게)

### Cypress 설치 및 실행

```bash
# 설치
npm install cypress --save-dev

# Cypress 실행
npx cypress open
```

### Cypress 테스트 케이스 예제

#### 테스트 1: 페이지 접속 테스트

```javascript
describe("Papago 번역 테스트", () => {
  it("페이지가 정상적으로 로드된다", () => {
    cy.visit("http://localhost:3000");
    cy.contains("번역기");
  });
});
```

#### 테스트 2: 번역 기능 테스트

```javascript
it("번역 기능이 정상적으로 동작한다", () => {
  cy.visit("http://localhost:3000");

  // 텍스트 입력
  cy.get("#source-text").type("Hello");

  // 번역 버튼 클릭
  cy.get("#translate-btn").click();

  // 번역 결과 확인
  cy.get("#target-text").should("contain", "안녕하세요");
});
```

#### 테스트 3: 언어 감지 테스트

```javascript
it("입력된 텍스트의 언어를 자동 감지한다", () => {
  cy.visit("http://localhost:3000");

  // 한국어 텍스트 입력
  cy.get("#source-text").type("안녕하세요");

  // 언어 감지 드롭다운이 'ko'로 변경되는지 검증
  cy.get("#source-lang").should("have.value", "ko");
});
```

#### 테스트 4: 다크모드 토글 테스트

```javascript
it("다크모드가 정상적으로 토글된다", () => {
  cy.visit("http://localhost:3000");

  // 다크모드 토글 클릭
  cy.get("#checkbox").click();

  // html 태그에 dark 클래스가 추가되는지 검증
  cy.get("html").should("have.class", "dark");
});
```

### 테스트 커버리지

- **라인 커버리지**: 코드의 몇 줄이 실행되었는지
- **분기 커버리지**: if/else 등의 분기문이 모두 실행되었는지
- 100% 커버리지라고 해도 모든 버그를 잡을 수는 없음
- **엣지 케이스**: 개발자가 고려하지 못한 경계값 케이스

### React 컴포넌트 테스팅

- **React Testing Library** 사용
- 컴포넌트가 화면에 잘 렌더링되는지 테스트
- 사용자 관점에서 테스트 작성

```javascript
import { render, screen } from "@testing-library/react";
import App from "./App";

test("renders learn react link", () => {
  render(<App />);
  const linkElement = screen.getByText(/learn react/i);
  expect(linkElement).toBeInTheDocument();
});
```

---

## 오늘의 총정리

### 0. npm & 프로젝트 실행

- package.json의 개념과 구조 이해
- dependencies vs devDependencies
- CLI 명령어 연습 (npm install, npm run dev 등)

### 1. 리팩토링

- XHR → fetch & async/await 변경
- 코드 가독성과 유지보수성 향상

### 2. key 관리

- .env 파일로 환경변수 관리
- .gitignore로 민감한 정보 보호
- key 노출 시나리오와 대응 방법

### 3. E2E 테스트

- Cypress를 이용한 E2E 테스트 작성
- 테스트 자동화의 필요성
- 테스트 피라미드 개념

---

## 참고 자료

- [npm 공식 문서](https://docs.npmjs.com/)
- [Cypress 공식 문서](https://www.cypress.io/)
- [React Testing Library](https://testing-library.com/react)
