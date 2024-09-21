---
title: '바닐라로 고양이 검색 만들기 : render() addEventListener에서 메서드 사용하기'
categories: [Javascript]
tags: [javascript, vanila]
---

{:toc .large-only}

render에서 다른 메서드를 호출하면 this.setState is not a function 에러가 뜬다.

```js
$close.addEventListener('click', this.handleClose);
```

```js
  handleClose() {
    console.log(this);
    this.setState({
      visible: false,
      image: null,
    });
  }
```

<br/>

handleClose에서 `console.log(this)`를 찍어보면 $close Node가 나온다.

`() => {this.handleClose()}` 혹은 `this.handleClose.bind(this)` 로 호출하면 콘솔에 제대로 ImageInfo 값이 나온다.

`$close.addEventListener`로 메서드를 호출하면 this가 $close가 되어 this.setState가 에러가 뜨는 것이었다.

> addEventListener 함수의 콜백 함수를 화살표 함수로 정의하면 this가 상위 컨택스트인 전역 객체 window를 가리킨다.

> bind() 메소드가 호출되면 새로운 함수를 생성합니다. 받게되는 첫 인자의 value로는 this 키워드를 설정하고, 이어지는 인자들은 바인드된 함수의 인수에 제공됩니다.

다른 메서드를 사용하는 메서드를 호출할 때는 바인딩 혹은 callback 함수를 사용해줘야 한다는 것을 기억하자..

<br/>

[addEventListener 함수의 콜백 함수](https://poiemaweb.com/es6-arrow-function#44-addeventlistener-%ED%95%A8%EC%88%98%EC%9D%98-%EC%BD%9C%EB%B0%B1-%ED%95%A8%EC%88%98)<br/>

[Function.prototype.bind()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)
