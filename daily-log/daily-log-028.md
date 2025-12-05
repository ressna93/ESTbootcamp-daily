# 2025년 12월 05일 — 프론트엔드 개발자 부트캠프 28일차 TIL

## 오늘의 목표

### JavaScript 기초 심화 학습 + DOM 조작 + 이벤트 흐름 이해

- 1교시 (09:00 ~ 10:00)
  JSON 데이터 & 배열 메서드 활용

> 서버로부터 받았다고 가정한 JSON 데이터를 파싱한 후 다음 메서드를 활용하여 처리했다.

1. filter() — 특정 조건의 상품만 추출

   > const electronicItems = productsData.filter(item => item.category === "전자기기");

2. map() — 상품 이름 배열 만들기

   > const names = productsData.map(item => item.name);

3. sort() — 가격 기준 내림차순 정렬
   > sort()는 원본 배열을 변경하므로 복사본 사용 권장

```js
const sortedByPrice = [...productsData].sort((a, b) => b.price - a.price);
```

4. 메서드 체이닝 예제

> 재고가 있는(stock > 0) 의류 상품만 가져와
> → 가격 오름차순 정렬
> → {name, price} 형태로 새 배열 생성

```js
const result = productsData
  .filter((item) => item.category === "의류" && item.stock > 0)
  .sort((a, b) => a.price - b.price)
  .map((item) => ({
    name: item.name,
    price: item.price,
  }));
```

- 문제 1: filter로 재고 있는 상품

```js
const inStockItems = productsData.filter((item) => item.stock > 0);
```

- 문제 2: map으로 가격만 추출

```js
const prices = productsData.map((item) => item.price);
```

- 문제 3: reduce로 총 재고 계산

```js
const totalStock = productsData.reduce((acc, item) => acc + item.stock, 0);
```

- 문제 4: 메서드 체이닝
  → 위의 의류 + stock + 정렬 + 매핑 예제 동일

- 2교시 (10:00 ~ 11:00)
  테이블 동적 생성 기초

> JavaScript로 HTML `<table>` 요소를 생성하고 DOM에 추가하는 방법 학습.

- 3교시 (11:00 ~ 12:00)
  테이블 동적 생성 실습

> createElement()
> appendChild()
> 반복문을 활용한 행(Row)·셀(Cell) 생성 실습 진행

- 4교시 (13:00 ~ 14:00)
  DOM 트리에 접근하기
  DOM API 란?

> HTML 문서를 트리 구조의 객체로 표현한 것
> JavaScript는 DOM을 통해 요소를 접근·수정·생성·삭제할 수 있음

1. ID로 요소 접근

```js
document.getElementById("myId");
```

2. CSS 선택자로 요소 접근

```js
document.querySelector(".item");
document.querySelectorAll("div.card");
```

3. 태그 이름 / 클래스 접근 (구식 방법)

```js
document.getElementsByTagName("div");
document.getElementsByClassName("box");
```

4. DOM 트리 순회
   parentNode, children, nextElementSibling 등을 활용해 요소 이동
   이벤트 흐름 (Event Flow)

1. 캡처링 단계 (위 → 아래)
   window → document → html → body → 부모요소들 → target

1. 버블링 단계 (아래 → 위)
   target → 부모 → body → html → document → window

- 5교시 (14:00 ~ 15:00)
  DOM 제어

1. 이벤트 삽입

```js
element.addEventListener("click", handler);
```

2. 클래스 제어

```js
element.classList.add("active");
element.classList.remove("active");
element.classList.toggle("active");
```

3. 요소 제어

```js
const div = document.createElement("div");
parent.appendChild(div);
element.remove();
```

6교시 (15:00 ~ 16:00) 4. 콘텐츠 조작

```js
element.textContent = "텍스트 변경";
element.innerHTML = "<strong>굵은 텍스트</strong>";
```

5. 스타일 제어

```js
element.style.color = "red";
element.style.backgroundColor = "#eee";
```

실습
요소 생성 및 추가
텍스트 변경, HTML 삽입

- 7교시 (16:00 ~ 17:00)
  > 이벤트 심화 — 전파, this, target
  > 캡처링과 버블링 차이
  >
  > 1.  캡처링: grandparent → parent → child
  > 2.  버블링: child → parent → grandparent
  >     event.target
  >     ➡ 클릭이 시작된 실제 요소
  >     event.currentTarget / this
  >     ➡ 이벤트리스너가 등록된 요소

```js
stopPropagation();
event.stopPropagation(); // 이벤트 전파 중단
preventDefault();
link.addEventListener("click", (e) => {
  e.preventDefault();
  alert("기본 동작(페이지 이동) 취소됨");
});
```

- 8교시 (17:00 ~ 18:00)
  이벤트 위임 (Event Delegation)
  핵심 패턴

```js
parent.addEventListener("click", (e) => {
  if (e.target.matches(".child")) {
    // 처리
  }
});

실제 예제
container.addEventListener("click", function (event) {
  if (event.target.classList.contains("item")) {
    const itemText = event.target.textContent;
    log.textContent = `"${itemText}" 클릭됨!`;
  }
});

동적 요소 추가
addItemBtn.addEventListener("click", function () {
  itemCount++;
  const newItem = document.createElement("div");
  newItem.classList.add("item");
  newItem.textContent = `아이템 ${itemCount}`;
  container.appendChild(newItem);
});
```

> 이벤트 위임의 장점
> 효율성 — 리스너 하나만 등록
> 동적 요소 처리 — 새로 추가된 요소도 자동 처리
> 유지보수 간편 — 코드 간결

오늘의 핵심 정리
JSON 데이터를 배열 메서드로 자유롭게 가공할 수 있다.
DOM 접근 방식: getElementById, querySelector 등 숙지
DOM 제어: 생성/삭제/클래스/스타일 조작 필수
이벤트 흐름(캡처링·버블링)을 이해해야 복잡한 UI 구현 가능
이벤트 위임은 리스트/동적 요소 처리의 필수 패턴
