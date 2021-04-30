---
layout: post
title: "배열의 얕은 복사와 깊은 복사"
sitemap: false
---

{:toc .large-only}

### 얕은 복사

#### 기본형에서 얕은 복사

기본형 타입에서는 복사한 데이터를 변경해도 원본은 변경되지 않는다.

```js
var a = "a";
var b = a;

b = "b";

console.log(a);
// 'a'
console.log(b);
// 'b'
```

<br/>

![코드에서 메모리 변화](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fc2CREj%2FbtqC3OPKKGv%2FQ9nTUlt1DuvpGPzv5c7fY1%2Fimg.jpg "두 변수는 서로 같은 주솟값을 참조하고 있음")<br/>
![코드에서 메모리 변화](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FrU6OR%2FbtqC5nRubs5%2FXxwA8hMPM1pLTA5x5nqX1k%2Fimg.jpg "원본의 주소를 참조하고 있었지만 새로운 데이터로 변경할 때 데이터 영역에서 새로운 데이터를 할당하고 그 주솟값을 다시 참조함")

#### 참조형에서 얕은 복사

```js
var arr1 = [1, 2, 3, 4];
var arr2 = arr1;

arr2[0] = 0;

console.log(arr1);
// [ 0, 2, 3, 4 ]
console.log(arr2);
// [ 0, 2, 3, 4 ]
```

<br/>

![코드에서 메모리 변화](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F7mSsi%2FbtqC22HGwPM%2Fk1jdxqC7ypkp27kG4jMTLK%2Fimg.jpg "두 변수는 서로 같은 주솟값을 참조하고 있음")<br/>
![코드에서 메모리 변화](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbfvTet%2FbtqC21opzVf%2Fw4KQ1szIw6WYZrN0d3JpVK%2Fimg.jpg "arr2 가 arr1 과 같은 배열을 참조하고 있기 때문에 사본인 arr2 에서 배열의 요소를 수정했을 때 원본에도 수정이 일어남. 즉, 원본을 가리키는 또 다른 식별자가 생겨난 것임(얕은 복사)")

<br/>

#### Array.prototype.slice()

- Array.prototype.slice() 를 사용하면 새로운 배열을 반환해준다.
- 배열 안에 참조형 요소가 있다면 얕은 복사가 된다.

```js
var arr1 = [1, 2, 3, 4];
var arr2 = arr1.slice();

arr2[0] = 0;

console.log(arr1);
// [ 1, 2, 3, 4 ]
console.log(arr2);
// [ 0, 2, 3, 4 ]
```

```js
var arr3 = [{ a: 1 }, { b: 2 }, 3, 4];
var arr4 = arr3.slice();

arr3[0].a = 0;

console.log(arr3);
// 'arr3: ' [ { a: 0 }, { b: 2 }, 3, 4 ]
console.log(arr4);
// 'arr4: ' [ { a: 0 }, { b: 2 }, 3, 4 ]
```

### 깊은 복사

#### JSON 객체의 메서드 사용

- 문자열(String)으로 변환되었다가 다시 객체(Object)로 변환되기 때문에 이전 객체에 대한 참조가 없어지는 원리를 이용
- 함수(functions), Date 객체, 정규표현식, gettser/setter 등 JSON 으로 변경할 수 없는 깊은 복사가 불가능한 타입들이 꽤 많다.
- 속도가 느려 성능이 떨어진다.

```js
var obj1 = {
  a: "hello",
  b: [1, 2, 3],
  c: { cc: "left" },
};

var obj2 = JSON.parse(JSON.stringify(obj1));
obj2.c.cc = "right";

console.log(obj1);
// { a: 'hello', b: [ 1, 2, 3 ], c: { cc: 'left' } }
console.log(obj2);
// { a: 'hello', b: [ 1, 2, 3 ], c: { cc: 'right' } }
```

<br/>

[JSON 객체의 메소드 이용](https://chaewonkong.github.io/posts/js-deep-copy.html#1-json-%EA%B0%9D%EC%B2%B4%EC%9D%98-%EB%A9%94%EC%86%8C%EB%93%9C-%EC%9D%B4%EC%9A%A9)

#### 커스텀 재귀 함수 사용

- 함수를 재귀적으로 실행해 깊은 복사(Deep Copy)를 실현
- 인수값이 객체가 아닌 경우는 그냥 반환하며, 객체인 경우 객체의 값 만큼 루프를 돌며 재귀를 호출하여 복사된 값을 반환

```js
function cloneObject(obj) {
  var clone = {};
  if (typeof obj === "object" && obj !== null) {
    for (var key in obj) {
      clone[key] = cloneObject(obj[key]);
    }
  } else {
    clone = obj;
  }
  return clone;
}

var obj1 = {
  a: 1,
  b: [1, 2, 3],
};
var obj2 = cloneObject(obj1);
obj2.b = [1, 2];

console.log(obj1);
// { a: 1, b: [ 1, 2, 3 ] }
console.log(obj2);
// { a: 1, b: [ 1, 2 ] }
```

<br/>
[얕은 복사, 깊은 복사](https://bbaktaeho-95.tistory.com/37)

#### lodash 라이브러리 사용

- lodash 라이브러리를 이용하는 방식
- lodash는 shallow copy를 지원하는 clone()과 deep copy를 지원하는 cloneDeep()이 있다.

```js
import * as _ from "lodash";

const original = { a: { b: 2 } };

let copy = _.cloneDeep(original);
copy.a.b = 100;

console.log(original.a.b);
// 2
```

<br/>

[Deepcopy를 지원할 것 같은 javascript Object copy 방법들](http://hochulshin.com/javascript-best-deepcopy/)
