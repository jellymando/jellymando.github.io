---
title: "자바스크립트 동작 원리, 메모리 구조, 이벤트 루프"
categories: [Javascript]
tags: [javascript, 이벤트 루프]
---

{:toc .large-only}

## 자바스크립트 엔진

- 자바스크립트 코드를 실행하는 프로그램 혹은 인터프리터

- 각각의 엔진이 서로 다른 웹 브라우저, Node.js와 같은 런타임 등에서 동작할 수 있다.

- javascript 대표 엔진으로는 Google V8 엔진이 있다.

## 메모리 구조

- `Memory Heap`

  - 메모리 할당이 일어나는 곳으로서 구조화되지 않은 넓은 메모리 영역을 지칭
  - 변수, 함수의 저장/호출 작업이 발생하는 메모리 공간

- `Call Stack`
  - 코드를 읽어내려가면서 실행할 함수를 밑에서부터 호출 스택을 하나씩 쌓고, 메모리 힙에서 작업 수행에 필요한 것들을 찾아서 작업을 수행하는 공간
  - 호출 스택의 각 항목을 스택 프레임이라고 한다.

<br/>

<img src="/assets/img/blog/2021-08-27-event-order_01.png">

### 메모리 구조 예시

```js
function Animal() {}
// stores `new Animal()` instance on memory address 0x001232
// tiger has 0x001232 as value in stack
const tiger = new Animal();
// stores `new Object()` instance on memory address 0x000001
// `lion` has 0x000001 as value on stack
let lion = {
  strength: "Very Strong",
};
```

tiger와 lion은 참조형 타입이다.

코드가 실행되다 `Animal()`의 인스턴스를 생성하면 Heap의 메모리 주소 어딘가에 저장된다.

변수 tiger는 스택에 쌓이게 되고 그 value로 `Animal()`의 Heap 메모리 주소를 갖게 된다.

즉, tiger 변수에 접근하면 value가 가리키고 있는 Heap 메모리 주소로 이동하고 거기에 저장된 value를 꺼내오는 것이다.

<br/>

<img src="/assets/img/blog/2021-08-27-event-order_02.png">

<br/>

<img src="/assets/img/blog/2021-08-27-event-order_02_2.png">

<br/>

## 동작 구조

- Web APIs : 브라우저에서 제공하는 API

- 이벤트 루프(Event Loop) : 콜 스택이 비어 있을 때 콜백 큐의 첫 번째 콜백을 넘겨준다.

<img src="/assets/img/blog/2021-08-27-event-order_03.png">

## 동작 순서

### 동기 방식 이벤트 처리

[1] javascript 엔진이 코드를 순차적으로 실행한다.

[2] 코드 실행 중 함수를 발견하면 콜 스택에 넣는다.

[3] 콜 스택에 넣은 함수를 실행한다.

[4] 실행된 함수는 콜 스택에서 제거한다.

### 비동기 방식 이벤트 처리

[1] javascript 엔진이 코드를 순차적으로 실행한다.

[2] 코드 실행 중 비동기 이벤트 발견시 이벤트 함수를 콜 스택에 넣는다.

[3] 비동기 이벤트 함수의 Event handler를 콜백 큐에 넣는다.

[4] 콜 스택이 비어 있을 경우 콜백 큐에서 Event handler 하나를 꺼내서 콜 스택에 넣는다.

[5] 콜 스택에 넣은 함수를 실행한다.

[6] 실행된 함수는 콜 스택에서 제거한다.

## 콜 스택 동작 예제

<img src="/assets/img/blog/2021-08-27-event-order_04.png">

<br/>

[1] 자바스크립트 파일이 실행되면서 동시에 (anonymous)라는 함수가 콜 스택의 가장 아래에 들어온다. 이를 Global Execution Context라고 하는데 나중에 자세히 살펴보자. 함수 이름이 (anonymous)인 이유는 자바스크립트 파일의 이름이 현재 없어서 그렇다.

[2] 가장 아래에 작성된 코드인 calculate() 함수를 읽음과 동시에 이 함수가 콜 스택에서 두번째 밑으로 들어온다. 그리고 이를 수행하기 위해 calculate() 함수가 선언된 코드 안 쪽으로 들어가게 된다.

[3] sumTotal을 계산해서 그 값을 얻어낸 후 다음 줄로 내려간다.

[4] 이 코드를 실행하기 위해서는 subtractTwo() 함수를 알아야하기에 당장 calculate() 함수가 콜 스택에서 제거되지 못하고, 대신 subtractTwo() 함수가 콜 스택에 새롭게 쌓인다. 그리고 이 함수를 실행하기 위해 함수가 정의된 곳으로 간다.

<br/>

<img src="/assets/img/blog/2021-08-27-event-order_05.png">

<br/>

[5] subtractTwo() 함수의 값을 계산하여 값 7을 얻어냈다.

[6] 계산된 값을 토대로 subtractTwo() 함수를 실행했으므로 이 함수는 콜 스택에서 제거된다.

[7] calculate() 함수 또한 실행에 필요한 모든 값을 얻었으므로, 실행되고 콜 스택에서 제거된다.

[8] 마지막으로 본 파일의 실행이 모두 끝났으므로 Global Execution Context인 (anonymous) 함수 또한 콜 스택에서 제거되고, 모든 수행이 종료된다.

## 콜백 큐 (비동기 이벤트) 동작 예제

```js
alert("A");
setTimeout(function () {
  alert("B");
}, 0);
alert("C");
// A, C, B
```

<br/>

[1] `alert('A')`를 콜 스택에 넣고 `alert`를 실행 후 콜 스택에서 제거

[2] `setTimeout` 을 콜 스택에 넣고 `setTimeout`의 Event handler를 콜백 큐에 넣은 후 `setTimeout`을 콜 스택에서 제거

[4] `alert('C')`를 콜 스택에 넣고 `alert` 실행 후 콜 스택에서 제거

[5] 콜 스택이 비어있을 경우 콜백 큐에서 Event handler 하나를 콜 스택에 넣은 후 콜백 큐에서 Event handler 하나를 제거

[6] 콜 스택에 존재하는 Event handler를 실행 후 콜 스택에서 제거

<br/>

<img src="/assets/img/blog/2021-08-27-event-order_06.png">

<br/>

```js
for (var i = 0; i < 3; i++) {
  setTimeout(function () {
    alert(i);
  }, 1000);
}
// 3, 3, 3
```

#### 1, 2, 3이 아닌 3, 3, 3이 출력되는 이유

javascript 엔진이 먼저 코드를 실행 후 비동기로 동작하는 setTimeout Web API 를 3번 실행하였기 때문에 현재 콜백 큐에는 3개의 Event Handler가 들어가있다.

그래서 모든 코드 실행 후 마지막으로 콜백 큐에 등록된 Event Handler가 처리되기 때문에 현재 for 문의 i 값이 3이므로 실행되는 Event handler는 3을 3번 출력하는 것이다.

## 참고사이트

[[javascript] 4. 자바스크립트 실행 순서](https://doitnow-man.tistory.com/m/128)<br/>
[자바스크립트의 동작원리: 엔진, 런타임, 호출 스택](https://joshua1988.github.io/web-development/translation/javascript/how-js-works-inside-engine/)<br/>
[자바스크립트 런타임 : 콜 스택과 메모리 힙](https://soldonii.tistory.com/53)<br/>
[JS 메모리 구조](https://velog.io/@code-bebop/JS-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EA%B5%AC%EC%A1%B0)
