---
title: "✅Virtual DOM이란? Diffing Algorithm"
categories: [React]
tags: [react, virtual dom]
---

{:toc .large-only}

## DOM

Virtual DOM에 대해 이해하려면 DOM부터 알아봐야 하겠다.

<img src="/assets/img/blog/2021-10-13-DOM_01.jpeg" style="margin:30px 0">

DOM은 Document Object Model의 약자로, <u>객체로 표현되는 문서(HTML 등) 구조</u>이다.

프로그래밍 언어가 DOM 구조에 접근할 수 있는 방법을 제공하여 문서 구조, 스타일, 내용 등을 변경할 수 있게 돕는다.

HTML은 정적이지만 자바스크립트를 이용하여 동적으로 변경할 수 있다.

자바스크립트에서는 요소 노드를 가져오는 다양한 방법을 제시한다.

예를 들면, `document.getElementById`, `document.getElementsByTagName`, `document.querySelector` 등이 있다.

<img src="/assets/img/blog/2021-10-13-DOM_02.jpeg" style="margin:30px 0">

DOM을 조작할 때마다 웹 페이지를 새로 그리면 성능이 저하될 수 있다.

이런 점을 해결하기 위해 리액트는 Virtual DOM 방식을 사용한다.

## Virtual DOM

리액트 공식 문서에 나와 있는 Virtual DOM에 대한 설명은 아래와 같다.

> Virtual DOM (VDOM)은 UI의 이상적인 또는 “가상”적인 표현을 메모리에 저장하고 ReactDOM과 같은 라이브러리에 의해 “실제” DOM과 동기화하는 프로그래밍 개념입니다. 이 과정을 재조정이라고 합니다.

> 이 접근방식이 React의 선언적 API를 가능하게 합니다. React에게 원하는 UI의 상태를 알려주면 DOM이 그 상태와 일치하도록 합니다. 이러한 방식은 앱 구축에 사용해야 하는 어트리뷰트 조작, 이벤트 처리, 수동 DOM 업데이트를 추상화합니다.

종합해서 해석하자면, 리액트는 Virtual DOM을 사용하여 **실제 DOM이 아닌 이를 추상화한 객체 DOM**을 메모리에 구성하여 사용한다.

Virtual DOM의 장점은 DOM을 최소한으로 조작하여 작업을 처리할 수 있다는 점이다.

## DOM 업데이트 과정

리액트에서 데이터가 변하여 웹 브라우저에 실제 DOM을 업데이트하는 과정

1. 데이터를 업데이트하면 전체 UI를 Virtual DOM에 리렌더링
1. 이전 Virtual DOM에 있던 내용과 현재 내용을 비교
1. **바뀐 부분만 실제 DOM에 적용**

## 비교 알고리즘 (Diffing Algorithm)

state나 props가 갱신되면 `render()` 함수는 새로운 React 엘리먼트 트리를 반환한다.

하나의 트리를 다른 트리로 변환하기 위한 최소한의 연산 수를 구하는 알고리즘은 n개의 엘리먼트가 있는 트리에 대해 O(n3)의 복잡도를 가진다.

React에 이 알고리즘을 적용한다면, 1000개의 엘리먼트를 그리기 위해 10억 번의 비교 연산을 수행해야 한다.

대신 React는 두 가지 가정을 기반하여 O(n) 복잡도의 휴리스틱 알고리즘을 구현한다.

1. 서로 다른 타입의 두 엘리먼트는 서로 다른 트리를 만들어낸다.
1. 개발자가 key prop을 통해, 여러 렌더링 사이에서 어떤 자식 엘리먼트가 변경되지 않아야 할지 표시해 줄 수 있다.

#### 엘리먼트의 타입이 다른 경우

두 루트 엘리먼트의 타입이 다르면, React는 이전 트리를 버리고 완전히 새로운 트리를 구축한다.

`<a>`에서 `<img>`로, `<Article>`에서 `<Comment>`로, 혹은 `<Button>`에서 `<div>`로 바뀌는 것 모두 트리 전체를 재구축하는 경우이다.

트리를 버릴 때 이전 DOM 노드들은 모두 파괴되며 루트 엘리먼트 아래의 모든 컴포넌트도 언마운트되고 그 state도 사라진다.

예를 들어 아래와 같이 변경되었을 때, 이전 Counter는 사라지고 새로 마운트된다.

```jsx
<div>
  <Counter />
</div>

<span>
  <Counter />
</span>
```

#### Keys

리스트의 맨 앞에 엘리먼트를 추가하는 경우 성능이 좋지 않다.

아래처럼 리스트가 변경되면 React는 ul의 모든 자식을 변경하며 이는 매우 비효율적이다.

```html
<ul>
  <li>Duke</li>
  <li>Villanova</li>
</ul>

<ul>
  <li>Connecticut</li>
  <li>Duke</li>
  <li>Villanova</li>
</ul>
```

이러한 문제를 해결하기 위해, React는 key 속성을 지원한다.

React는 key를 통해 기존 트리와 이후 트리의 자식들이 일치하는지 확인한다.

```html
<ul>
  <li key="2015">Duke</li>
  <li key="2016">Villanova</li>
</ul>

<ul>
  <li key="2014">Connecticut</li>
  <li key="2015">Duke</li>
  <li key="2016">Villanova</li>
</ul>
```

이제 React는 '2014' key를 가진 엘리먼트가 새로 추가되었고, '2015'와 '2016' key를 가진 엘리먼트는 그저 이동만 하면 된다.

해당 key는 오로지 형제 사이에서만 유일하면 되고, 전역에서 유일할 필요는 없다.

## 참고사이트

[(번역) DOM은 정확히 무엇일까?](https://wit.nts-corp.com/2019/02/14/5522)<br/>
[Virtual DOM과 Internals](https://ko.reactjs.org/docs/faq-internals.html)<br/>
[문서객체모델 DOM이란? 자바스크립트가 HTML을 다루기 위한 문서모델](https://oursmalljoy.com/%EB%AC%B8%EC%84%9C%EA%B0%9D%EC%B2%B4%EB%AA%A8%EB%8D%B8-dom%EC%9D%80-%EB%AC%B4%EC%97%87%EC%9D%B4%EA%B3%A0-%ED%95%84%EC%9A%94%ED%95%9C-%EC%9D%B4%EC%9C%A0/)

- 리액트를 다루는 기술 39p
