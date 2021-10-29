---
layout: post
title: "Class와 함수 생성자의 차이"
sitemap: false
---

{:toc .large-only}

## Class

- ES6에서 추가된 객체 생성 템플릿 함수

### Constructor (생성자)

- 객체를 생성하고 초기화하기 위한 메서드

- 클래스 안에 한 개만 존재할 수 있다.

- 부모 클래스의 constructor를 호출하기 위해 super 키워드를 사용할 수 있다.

```js
class User {
  constructor(name) {
    this.name = name;
  }

  sayHi() {
    alert(this.name);
  }
}

// 사용법:
let user = new User("John");
user.sayHi();
```

- 위 코드에서 `new User("John")`를 호출하면 다음과 같은 일이 일어난다.

1. 새로운 객체가 생성된다.
1. 넘겨받은 인수와 함께 constructor가 자동으로 실행되어 "John"이 `this.name`에 할당된다.
1. `user.sayHi()` 객체 메서드를 호출한다.

- user를 콘솔에 찍어보면 `name: "John"` 객체가 나오고, Prototype에 constructor, sayHi가 들어온다.

정리하자면,

```js
class User {
  constructor(name) {
    this.name = name;
  }
  sayHi() {
    alert(this.name);
  }
}

// 클래스는 함수입니다.
alert(typeof User); // function

// 정확히는 생성자 메서드와 동일합니다.
alert(User === User.prototype.constructor); // true

// 클래스 내부에서 정의한 메서드는 User.prototype에 저장됩니다.
alert(User.prototype.sayHi); // alert(this.name);

// 현재 프로토타입에는 메서드가 두 개입니다.
alert(Object.getOwnPropertyNames(User.prototype)); // constructor, sayHi
```

## 클래스는 프로토타입의 문법적 설탕인가?

ES5에서는 클래스 없이도 생성자 함수와 프로토타입을 통해 객체지향 언어의 상속을 구현할 수 있었다.

하지만 ES6에서 도입된 클래스는 클래스 기반 객체지향 프로그래밍 언어와 매우 흡사한 새로운 객체 생성 메커니즘을 제시한다.

클래스는 프로토타입 기반 패턴을 클래스 기반 패턴처럼 사용할 수 있도록 하는 문법적 설탕이라고 볼 **수도** 있다.

**단, 클래스와 생성자 함수는 모두 프로토타입 기반의 인스턴스를 생성하지만 클래스는 생성자 함수보다 엄격하며 생성자 함수에서는 제공하지 않는 기능도 제공한다.**

따라서 클래스를 프로토타입 기반 객체 생성 패턴의 단순한 문법적 설탕이라기 보다는 새로운 객체 생성 메커니즘으로 보는 것이 좀 더 합당하다.

## Class와 함수 생성자의 차이

1. 문법의 차이

```js
function Person({ name, age }) {
  this.name = name;
  this.age = age;
}
Person.prototype.introduce = function () {
  return `안녕하세요, 제 이름은 ${this.name}입니다.`;
};

class Person {
  constructor({ name, age }) {
    this.name = name;
    this.age = age;
  }

  // 객체에서 메소드를 정의할 때 사용하던 문법을 그대로 사용하면, 메소드가 자동으로 `Person.prototype`에 저장됩니다.
  introduce() {
    return `안녕하세요, 제 이름은 ${this.name}입니다.`;
  }
}
```

1. 클래스로 만든 함수엔 특수 내부 프로퍼티인 `[[FunctionKind]]: "classConstructor"`가 있어 new 연산자 없이 호출하면 에러가 발생한다.
1. 클래스는 상속을 지원하는 extends와 super 키워드를 제공한다.
1. 클래스는 호이스팅이 발생하지 않는 **것처럼** 동작하지만 함수 선언문으로 정의된 생성자 함수는 함수 호이스팅이 발생한다.
1. 클래스의 constructor, 메서드는 프로퍼티 어트리뷰트 `[[Enumerable]]`의 값이 false다. 즉, 열거되지 않는다.
1. 클래스 내부의 코드는 항상 strick mode로 실행되며 해제할 수 없다.

## 참고사이트

[Classes](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Classes#%ED%94%84%EB%A1%9C%ED%86%A0%ED%83%80%EC%9E%85_%EB%A9%94%EC%84%9C%EB%93%9C)<br/>
[클래스와 기본 문법](https://ko.javascript.info/class)<br/>
[클래스](https://helloworldjavascript.net/pages/270-class.html)<br/>
모던 자바스크립트 Deep Dive - 471p
