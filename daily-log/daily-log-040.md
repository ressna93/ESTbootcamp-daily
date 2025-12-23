# 2025년 12월 23일 - 프론트엔드 부트캠프 40일차

## 학습 주제

HTTP 프로토콜의 이해와 실습

---

## 1교시 (09:00~10:00) - HTTP 개요

### HTTP의 등장 배경

- 팀 버너스리의 제안으로 HTTP 탄생
- 웹의 기반이 되는 통신 프로토콜

### FTP와 HTTP의 차이

- RFC(Request for Comments) 표준 문서에 대한 이해

---

## 2교시 (10:00~11:00) - HTTP의 발전

### HTTP/1.1

- 현재 가장 많이 사용되는 프로토콜
- Keep-Alive, 파이프라이닝 지원

### OSI 7계층

- 네트워크 통신의 계층 구조 학습

---

## 3교시 (11:00~12:00) - HTTP 통신 실습

### APIDOG를 활용한 실습

- 서버 실행 후 HTTP 요청/응답 테스트
- 프론트엔드 개발자 관점에서의 HTTP 통신 이해
  - 서버 로직보다는 요청/응답 패턴에 집중
  - 실제 개발 환경을 가정한 실습

---

## 4교시 (13:00~14:00) - Accept 헤더

### Accept 헤더의 역할

클라이언트가 선호하는 응답 데이터 포맷을 서버에게 알려주는 헤더

### Content Negotiation (콘텐츠 협상)

```
Accept: text/html;q=1.0, application/json;q=0.8
```

**우선순위 처리 방식:**

1. 클라이언트가 HTML을 가장 선호하는 경우
2. 서버가 HTML 응답이 가능하면 → HTML로 응답
3. 서버가 HTML 응답이 불가능하면 → 다음 가중치인 JSON으로 응답

### 실습 내용

- HEADER 실험용 엔드포인트 테스트
- Accept 협상 시나리오 테스트

---

## 5교시 (14:00~15:00) - Content-Type 헤더

### Content-Type 시나리오 테스트

1. **요청 body의 타입 해석 테스트**

   - 서버가 Content-Type을 어떻게 해석하는지 확인

2. **HTML 렌더링 테스트**

   - `Content-Type: text/plain`으로 HTML 전송 시 렌더링 비교
   - 정상 렌더링과의 차이점 확인

3. **Content-Type 생략 테스트**
   - 헤더를 생략했을 때 브라우저의 동작 확인

### Content-Type 예시

```
Content-Type: text/html; charset=utf-8
Content-Type: multipart/form-data; boundary=something
```

### Cookie와 Session

**Cookie**

- 브라우저에 저장되는 Key:Value 형태의 데이터
- 다양한 용도로 활용

**Session**

- 로그인 상태 등을 유지하기 위한 메커니즘
- "세션이 만료되었습니다" → 로그인 페이지 유지 시간 관리

**In-memory 저장소**

- 서버 프로세스가 실행되는 동안만 유지되는 임시 저장소
- 메모리 vs 디스크 차이점 이해

---

## 6교시 (15:00~16:00) - Cookie를 활용한 인증

### 세션 기반 인증 플로우

**서버의 세션 저장 구조:**

```javascript
{
  'sessionId': 'B5ya123asdvqweasd..',
  'userId': 'ddd',
  'username': 'ddd',
  'createdAt': '1223, 14:44분'
}
```

### 인증 프로세스

1. **로그인 성공 시**

   - 서버가 세션 ID를 생성
   - `Set-Cookie` 헤더를 통해 브라우저에 세션 쿠키 저장

2. **인증이 필요한 요청 시**

   - 브라우저가 자동으로 쿠키를 요청에 포함
   - "내 정보보기" 등의 요청에 세션 쿠키 첨부

3. **서버의 인증 확인**

   - 요청 헤더에서 쿠키 추출
   - 세션 저장소에서 해당 세션 ID 검색

4. **응답 처리**
   - 인증 상태 확인 후 적절한 페이지 응답

### 추천 HTTP 헤더 학습 주제

- Location
- Referer
- Origin
- Keep-Alive
- Authorization
- Cache-Control, ETag (캐싱)

### CORS 관련 헤더

- Access-Control-Allow-Origin
- Access-Control-Allow-Headers

---

## 7교시 (16:00~17:00) - 주요 HTTP 헤더 심화

### ⭐⭐ Location 헤더 ⭐⭐

**사용되는 상태 코드:** 301, 302, 307, 308

**역할:** 서버가 클라이언트에게 "이 주소 말고 여기로 다시 요청해"라고 지시

**Location 헤더 301 코드 실습**

- 직접 코드 작성 및 발표
- 리다이렉션 동작 확인

### ⭐⭐Cache-Control 헤더 ⭐⭐

**주요 값:**

- `no-store`: 캐시 저장 금지
- `no-cache`: 캐시 사용 전 재검증
- `max-age=초`: 캐시 유효 시간
- `public` / `private`: 캐시 공유 범위

**역할:** 브라우저/프록시/CDN에게 응답 캐싱 정책 지시

---

## 8교시 (17:00~18:00) - HTTP 총정리

### 1. 기본 개념

- **클라이언트-서버 프로토콜**: 브라우저와 웹 서버 간의 통신 규약
- **무상태(Stateless)**: 각 요청이 독립적, 이전 요청을 기억하지 않음
- **텍스트 기반**: 사람이 읽을 수 있는 형태

### 2. HTTP 메서드

| 메서드  | 용도                        |
| ------- | --------------------------- |
| GET     | 데이터 조회                 |
| POST    | 데이터 생성                 |
| PUT     | 데이터 전체 수정            |
| PATCH   | 데이터 부분 수정            |
| DELETE  | 데이터 삭제                 |
| HEAD    | 헤더 정보만 조회            |
| OPTIONS | 서버가 지원하는 메서드 확인 |

### 3. 상태 코드

- **1xx**: 정보 응답
- **2xx**: 성공 (200 OK, 201 Created)
- **3xx**: 리다이렉션 (301 Moved Permanently, 302 Found)
- **4xx**: 클라이언트 오류 (400 Bad Request, 401 Unauthorized, 404 Not Found)
- **5xx**: 서버 오류 (500 Internal Server Error, 503 Service Unavailable)

### 4. HTTP 메시지 구조

**요청(Request)**

```http
GET /index.html HTTP/1.1
Host: www.example.com
User-Agent: Mozilla/5.0
Accept: text/html

[요청 본문 - POST 등에서 사용]
```

**응답(Response)**

```http
HTTP/1.1 200 OK
Content-Type: text/html
Content-Length: 1234

[응답 본문 - HTML, JSON 등]
```

### 5. 주요 헤더

- **Content-Type**: 데이터 형식 (application/json, text/html)
- **Content-Length**: 본문 크기
- **Authorization**: 인증 정보
- **Cookie/Set-Cookie**: 쿠키 정보
- **Cache-Control**: 캐싱 정책
- **User-Agent**: 클라이언트 정보

### 6. HTTP 버전

| 버전     | 특징                             |
| -------- | -------------------------------- |
| HTTP/1.0 | 연결당 하나의 요청/응답          |
| HTTP/1.1 | Keep-Alive, 파이프라이닝         |
| HTTP/2   | 멀티플렉싱, 헤더 압축, 서버 푸시 |
| HTTP/3   | QUIC 프로토콜 기반 (UDP)         |

### 7. HTTPS

- HTTP + SSL/TLS 암호화
- 포트 443 사용 (HTTP는 80)
- 데이터 보안 및 무결성 보장

### 8. HTTP의 특징

- **무상태성(Stateless)**

  - 확장성이 좋음
  - 상태 관리 필요 시 쿠키/세션 사용

- **비연결성(Connectionless)**
  - 요청-응답 후 연결 종료
  - 리소스 절약

---

## 오늘의 학습 성과

1. HTTP 프로토콜의 기본 개념과 동작 원리 이해
2. APIDOG를 활용한 실제 HTTP 요청/응답 실습
3. Accept, Content-Type 헤더의 역할과 Content Negotiation 학습
4. Cookie와 Session을 활용한 인증 메커니즘 이해
5. Location, Cache-Control 등 주요 HTTP 헤더 실습
6. HTTP 메서드, 상태 코드, 메시지 구조 총정리

---

## 참고 자료

- [MDN - Content-Type](https://developer.mozilla.org/ko/docs/Web/HTTP/Reference/Headers/Content-Type)
- RFC 문서 (HTTP 표준)
