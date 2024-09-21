---
title: "버블링과 캡쳐링 (feat. 흑역사)"
categories: [Javascript]
tags: [javascript, 버블링, 캡쳐링]
---

{:toc .large-only}

## 이벤트 전달 및 DOM 이벤트 흐름

이벤트가 통과하는 전파 경로는 문서의 계층적 트리 구조를 반영한다.

이벤트 단계에는 캡처 단계, 목표 단계 및 버블 단계의 세 가지가 있다.

단계가 지원되지 않거나 이벤트 객체의 전파가 중지된 경우 단계를 건너뛴다.

> 캡처 단계 : 조상을 통해 이벤트 객체의 대상의 부모까지 순서대로 내려오는 단계

> 타깃(target) 단계 : 이벤트 객체의 도착 이벤트 대상. 이벤트 객체는 이 단계의 완료 후 정지한다.

> 버블 단계 : 대상의 부모에서 시작하여 역순으로 올라가 조상에서 끝나는 단계

<img src="https://www.w3.org/TR/DOM-Level-3-Events/images/eventflow.svg" style="margin-top: 40px">

<br/>

위 그림에서 `<td>`를 클릭하면 이벤트가 최상위 조상에서 시작해 아래로 전파되고(캡처링 단계), 이벤트가 타깃 요소에 도착해 실행된 후(타깃 단계), 다시 위로 전파된다(버블링 단계).

## 버블링

한 요소에 이벤트가 발생하면 이 요소에 할당된 핸들러가 동작하고, 가장 최상단의 조상 요소를 만날 때까지 타고 올라가며 부모 요소의 핸들러가 동작한다.

아래 코드에서 `<p>`를 클릭하여 이벤트 버블링을 발생시키면 `P → DIV → FORM → BODY → HTML` 순서대로 alert이 호출된다.

```html
<style>
  body * {
    margin: 10px;
    border: 1px solid blue;
  }
</style>

<form>
  FORM
  <div>
    DIV
    <p>P</p>
  </div>
</form>

<script>
  for (let elem of document.querySelectorAll("*")) {
    elem.addEventListener("click", (e) => alert(`버블링: ${elem.tagName}`));
  }
</script>
```

<br/>

> <u>거의</u> 모든 이벤트는 버블링 되지만 focus 이벤트와 같이 버블링 되지 않는 이벤트도 있다.

## 캡쳐링

`on<event>` 프로퍼티나 HTML 속성, `addEventListener(event, handler)`를 이용해 할당된 핸들러는 캡처링에 대해 전혀 알 수 없다.

이 핸들러들은 타깃 단계와 버블링 단계에서만 동작하며 캡처링 단계에서 이벤트를 잡아내려면 addEventListener의 capture 옵션을 true로 설정해야 한다.

```js
elem.addEventListener(..., {capture: true})
// 아니면, 아래와 같이 true만 입력한다.
elem.addEventListener(..., true)
```

<br/>

아래 코드에서 `<p>`를 클릭하여 이벤트 캡쳐링을 발생시키면 `HTML → BODY → FORM → DIV → P` 순서대로 alert이 호출된다.

```html
<style>
  body * {
    margin: 10px;
    border: 1px solid blue;
  }
</style>

<form>
  FORM
  <div>
    DIV
    <p>P</p>
  </div>
</form>

<script>
  for (let elem of document.querySelectorAll("*")) {
    elem.addEventListener(
      "click",
      (e) => alert(`캡쳐링: ${elem.tagName}`),
      true
    );
  }
</script>
```

## 버블링/캡쳐링 중단하기

`event.stopPropagation()`을 사용하면 현재 이벤트 이후의 전파를 막는다.

이벤트 버블링의 경우에는 클릭한 요소의 이벤트만 발생시키고 상위 요소로 이벤트를 전달하지 않는다.

이벤트 캡쳐의 경우에는 클릭한 요소의 최상위 조상 요소의 이벤트만 발생시키고 하위 요소들로 이벤트를 전달하지 않는다.

위에서 살펴본 버블링과 캡쳐링의 예제 코드에 `event.stopPropagation()`을 추가하면 버블링은 `P`에서, 캡쳐링은 `HTML`에서 핸들러가 동작한다.

```js
item.addEventListener("click", function (e) {
  e.stopPropagation();
  e.target.classList.toggle("selected");
});
document.body.addEventListener("click", function (e) {
  items.forEach(function (elem) {
    elem.classList.remove("selected");
  });
});
```

위 예제에서 `item.addEventListener` 안에 `e.stopPropagation()`을 추가하지 않으면 이벤트가 버블링되어 body에서 selected 클래스가 다시 remove 된다.

> 꼭 필요한 경우가 아니라면 이벤트 버블링/캡쳐링을 중단하지 않는 것이 좋다.

## 참고사이트

[Event.stopPropagation ()](https://developer.mozilla.org/ko/docs/Web/API/Event/stopPropagation)<br/>
[이벤트 전달 및 DOM 이벤트 흐름](https://www.w3.org/TR/DOM-Level-3-Events/#event-flow)<br/>
[event.stopPropagation(), event.preventDefault () 이해하기](https://ismydream.tistory.com/98)<br/>
[이벤트 버블링, 이벤트 캡처 그리고 이벤트 위임까지](https://joshua1988.github.io/web-development/javascript/event-propagation-delegation/)
