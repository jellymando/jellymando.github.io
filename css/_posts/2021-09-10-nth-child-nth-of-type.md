---
layout: post
title: "가상 셀렉터 :nth-child와 :nth-of-type의 차이"
sitemap: false
---

{:toc .large-only}

## :nth-child

부모의 n번째 자식 요소

<img src="/assets/img/blog/2021-09-10-nth-child-nth-of-type_01.png">

## :nth-of-type

부모의 자식 요소 중 **type 조건을 만족하는** n번째 자식 요소

<img src="/assets/img/blog/2021-09-10-nth-child-nth-of-type_02.png">

## 무엇이 다른가?

```html
<div>
  <h1>Heading1</h1>
  <p>Lorem</p>
  <p>ipsum</p>
  <p>dolor</p>
</div>
```

위의 HTML 코드상에서 p에 `nth-child(2)`와 `nth-of-type(n)`을 적용했을 때 어떻게 나올까?

### nth-child(2)를 적용했을 때

<img src="/assets/img/blog/2021-09-10-nth-child-nth-of-type_03.png" style="margin-bottom:20px">

실제로 p 요소들 중에서는 첫번째이지만 div의 자식 중 두번째 요소에 적용되었다.

그러나 만약 HTML 구조가 아래와 같다면,

```html
<style>
  p {
    padding: 10px;
    border: 1px solid #d6d6d6;
  }
  p:nth-child(2) {
    background: orange;
  }
  p:last-child {
    background: violet;
  }
  p:nth-of-type(2) {
    background: orange;
  }
  p:last-of-type {
    background: violet;
  }
</style>
<div>
  <p>Lorem</p>
  <h1>Heading1</h1>
  <p>ipsum</p>
  <p>dolor</p>
  <h1>Heading1</h1>
</div>
```

<br/>

부모의 두번째 자식 요소는 h1이므로 p의 background가 바뀌지 않는다.

last-child도 마찬가지다.

<img src="/assets/img/blog/2021-09-10-nth-child-nth-of-type_05.png" style="margin-top:10px; width: 300px; height: auto;">
 
흥미롭다. p 요소와 상관없이 부모에게서 n번째 요소를 먼저 찾고, p면 적용된다.

**즉, 부모의 n번째 요소가 p면 css가 적용된다.**

MDN에도 이 예제가 나와 있다.

<img src="/assets/img/blog/2021-09-10-nth-child-nth-of-type_07.png" style="border:1px solid #d7d7d7;">

> 3 is used in the counting because it is a child, but it isn't selected because it isn't a `<span>`

### nth-of-type(2)를 적용했을 때

<img src="/assets/img/blog/2021-09-10-nth-child-nth-of-type_04.png" style="margin-bottom:20px">

**부모의 p요소 중 n번째 요소에 css를 적용한다.**

위에서 본 예외 예제에 적용해보면 형제와의 순서에 상관없이 p 요소 중에서 n번째 요소에 적용된다.

<img src="/assets/img/blog/2021-09-10-nth-child-nth-of-type_06.png" style="margin-top:10px; width: 300px; height: auto;">

참고로 선택자 없이 `:nth-of-type(n)`만 사용하는 것도 가능하다.

```css
article :first-of-type {
  background-color: pink;
}
```

## 참고사이트

[:nth-child](https://developer.mozilla.org/ko/docs/Web/CSS/:nth-child)<br/>
[:first-of-type](https://developer.mozilla.org/ko/docs/Web/CSS/:first-of-type)<br/>
[CSS 가상 클래스 셀렉터 :nth-child와 :nth-of-type의 차이점](https://hogni.tistory.com/112)
