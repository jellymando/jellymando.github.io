---
title: "이벤트 위임에서 button의 자식 node 클릭 시 이벤트 발생❎"
categories: [Javascript]
tags: [javascript]
---

{:toc .large-only}

TodoList를 만들며 container element에 클릭 이벤트를 위임해주었다.

```js
this.containerEl.addEventListener("click", ({ target }) => {
      if (target.id === "add-user-button") {
        return this.addUserButtonClickHandler();
      }
```

<br/>
그러나 #add-user-button 안에 span 태그가 있었고, 이 span 태그를 눌렀을 때는 `this.addUserButtonClickHandler()` 이벤트가 발생하지 않았다.

(span 태그에 "add-user-button" id값이 없으니까)

그렇다고 if문 안에 `if (target.id === "add-user-button" || target.nodeName = "SPAN" ...` 이런식으로 button 안의 모든 자식에 대해 집어넣는 것은 너무 비효율적이다.

#### 해결방법

1. css를 통한 해결

```css
span {
  pointer-events: none;
}
```

css를 통해 포인터 이벤트 속성을 수정한다.

다만 익스플로러 등의 브라우저 버전이 낮으면 불가능하다.

2. js를 통한 해결

```js
this.containerEl.addEventListener("click", (e) => {
  let target = e.target;
  while (target.nodeName !== "BUTTON") {
    target = e.target.parentNode;
    if (target.nodeName === "BODY") return (target = null);
  }
  if (target.id === "add-user-button") {
    return this.addUserButtonClickHandler();
  }
});
```

button의 자식을 클릭했을 때 while문으로 target을 parentNode로 교체한다.

parentNode.nodeName이 body일 때는 리턴한다.

실행해봤는데 버튼 외 다른 요소들을 클릭했을 때 계속 parentNode를 추적하기 때문에 페이지가 굉장히 느려진다..
<br/>

[[javascript]이벤트 위임(event delegation)](https://juein.tistory.com/63)<br/>
[pointer-events(CSS)](https://developer.mozilla.org/ko/docs/Web/CSS/pointer-events)
