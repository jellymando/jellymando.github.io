---
layout: post
title: "props로 전달받은 메서드 this 바인딩"
sitemap: false
---

{:toc .large-only}

바닐라 투두리스트 만들면서 app에서 내려받은 메서드 실행 안됨..

app에 있는 메서드 내의 `this.render()` 에서 this가 자식놈 컴포넌트로 전달됨..

app에서 자식놈한테 물려줄 때부터 `this.setItem.bind(this)` 이런 식으로 바인딩 하고 물려줘야 함

```js
setItem() {
localStorage.setItem("item", JSON.stringify(this.todoData));
this.render();
}

this.todoInput = new TodoInput({
    todoData: this.todoData,
    todoSet: this.setItem.bind(this),
});
```
