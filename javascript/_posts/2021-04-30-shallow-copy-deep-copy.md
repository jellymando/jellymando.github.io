---
layout: post
title: 'immutable 데이터와 mutable 데이터, 얕은 복사/깊은 복사'
sitemap: false
---

{:toc .large-only}

## immutable 데이터와 mutable 데이터

### immutable 데이터

immutable은 **불변**이라는 뜻이며 boolean, number, string 등의 기본형 데이터는 immutable하다.

```js
var v1 = 'test'
var v2 = v1

console.log(v1)
// 'test'
console.log(v2)
// 'test'
```

위 예시에서 v2 변수에 v1 값을 할당한다.

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fc2CREj%2FbtqC3OPKKGv%2FQ9nTUlt1DuvpGPzv5c7fY1%2Fimg.jpg" style="margin:20px 0;" />

'test'라는 string 타입 데이터가 기존 주소값에 없기 때문에 새로 할당된다.

v1과 v2는 'test'라는 같은 string 값을 가지므로 같은 주소값을 참조한다.

```js
var v1 = 'test'
var v2 = v1
v1 = 'hi teaho'

console.log(v1)
// 'hi teaho'
console.log(v2)
// 'test'
```

위 코드에서는 v1의 값을 'hi teaho'로 변경했다.

v2는 v1을 복사한 것이니 v1 값을 바꾸면 v2 값도 바뀔까?

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FrU6OR%2FbtqC5nRubs5%2FXxwA8hMPM1pLTA5x5nqX1k%2Fimg.jpg" style="margin:20px 0;" />

'hi teaho'라는 string 타입 데이터가 기존 주소값에 없기 때문에 새로운 주소에 할당된다.

'test'와 'hi teaho'의 주소값이 각각 존재하기 때문에 이제 v1과 v2는 다른 주소값을 참조한다.

**기본형 타입에서는 복사한 데이터를 변경('hi teaho')해도 원본('test')은 변경되지 않는다. (immutable)**

### mutable 데이터

mutable은 변할 수 있다는 뜻이며 객체, 배열 등의 참조형 데이터는 mutable하다.

```js
var arr1 = [1, 2, 3, 4]
var arr2 = arr1

console.log(arr1)
// [ 1, 2, 3, 4 ]
console.log(arr2)
// [ 1, 2, 3, 4 ]
```

위 예시에서 arr2 변수에 arr1 값을 할당한다.

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F7mSsi%2FbtqC22HGwPM%2Fk1jdxqC7ypkp27kG4jMTLK%2Fimg.jpg" style="margin:20px 0;" />

'[ 1, 2, 3, 4 ]'라는 object 타입 데이터가 기존 주소값에 없기 때문에 새로 할당된다.

배열 안의 '1, 2, 3, 4'라는 number 타입 데이터가 기존 주소값에 없기 때문에 새로 할당되고, object 타입 데이터는 이 주소값들을 참조한다.

arr1과 arr2는 서로 같은 주소값을 참조한다.

```js
var arr1 = [1, 2, 3, 4]
var arr2 = arr1
arr2[0] = 0

console.log(arr1)
// [ 0, 2, 3, 4 ]
console.log(arr2)
// [ 0, 2, 3, 4 ]
```

arr2 배열의 첫번째 항목을 바꿔보자.

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbfvTet%2FbtqC21opzVf%2Fw4KQ1szIw6WYZrN0d3JpVK%2Fimg.jpg" style="margin:20px 0;" />

`0`이라는 number 타입 데이터가 기존 주소값에 없기 때문에 새로 할당되고, object 타입 데이터는 <u>새로운 주소에 할당되는 것이 아니라</u> '1' 데이터를 참조하던 항목의 주소값을 '0'을 참조하는 것으로 변경한다.

arr1과 arr2가 여전히 같은 주소값을 참조하기 때문에 같은 값을 가진다.

## mutable 데이터 얕은 복사

### Array.prototype.slice()

- Array.prototype.slice() 를 사용하면 새로운 배열을 반환해준다.
- 배열 안에 참조형 요소가 있다면 얕은 복사가 된다.

```js
var arr1 = [1, 2, 3, 4]
var arr2 = arr1.slice()

arr2[0] = 0

console.log(arr1)
// [ 1, 2, 3, 4 ]
console.log(arr2)
// [ 0, 2, 3, 4 ]
```

```js
var arr3 = [{ a: 1 }, { b: 2 }, 3, 4]
var arr4 = arr3.slice()

arr3[0].a = 0

console.log(arr3)
// 'arr3: ' [ { a: 0 }, { b: 2 }, 3, 4 ]
console.log(arr4)
// 'arr4: ' [ { a: 0 }, { b: 2 }, 3, 4 ]
```

## mutable 데이터 깊은 복사 (immutable)

### JSON.parse(JSON.stringify(obj))

- 문자열(String)으로 변환되었다가 다시 객체(Object)로 변환되기 때문에 이전 객체에 대한 참조가 없어지는 원리를 이용
- 함수(functions), Date 객체, 정규표현식, gettser/setter 등 JSON 으로 변경할 수 없는 깊은 복사가 불가능한 타입들이 꽤 많다.
- 속도가 느려 성능이 떨어진다.

```js
var obj1 = {
  a: 'hello',
  b: [1, 2, 3],
  c: { cc: 'left' }
}

var obj2 = JSON.parse(JSON.stringify(obj1))
obj2.c.cc = 'right'

console.log(obj1)
// { a: 'hello', b: [ 1, 2, 3 ], c: { cc: 'left' } }
console.log(obj2)
// { a: 'hello', b: [ 1, 2, 3 ], c: { cc: 'right' } }
```

[JSON 객체의 메소드 이용](https://chaewonkong.github.io/posts/js-deep-copy.html#1-json-%EA%B0%9D%EC%B2%B4%EC%9D%98-%EB%A9%94%EC%86%8C%EB%93%9C-%EC%9D%B4%EC%9A%A9)

### 재귀 함수 사용

- 함수를 재귀적으로 실행해 깊은 복사(Deep Copy)를 실현
- 인수값이 객체가 아닌 경우는 그냥 반환하며, 객체인 경우 객체의 값 만큼 루프를 돌며 재귀를 호출하여 복사된 값을 반환

```js
function cloneObject(obj) {
  var clone = {}
  if (typeof obj === 'object' && obj !== null) {
    for (var key in obj) {
      clone[key] = cloneObject(obj[key])
    }
  } else {
    clone = obj
  }
  return clone
}

var obj1 = {
  a: 1,
  b: [1, 2, 3]
}
var obj2 = cloneObject(obj1)
obj2.b = [1, 2]

console.log(obj1)
// { a: 1, b: [ 1, 2, 3 ] }
console.log(obj2)
// { a: 1, b: [ 1, 2 ] }
```

[얕은 복사, 깊은 복사](https://bbaktaeho-95.tistory.com/37)

### lodash 라이브러리 사용

- lodash 라이브러리를 이용하는 방식
- lodash는 shallow copy를 지원하는 `clone()`과 deep copy를 지원하는 `cloneDeep()`이 있다.

```js
import * as _ from 'lodash'

const original = { a: { b: 2 } }

let copy = _.cloneDeep(original)
copy.a.b = 100

console.log(original.a.b)
// 2
```

### structuredClone()

structuredClone는 자바스크립트의 네이티브 함수(내장 함수)이다.

```js
const original = {
  site: 'https://blog.openreplay.com/',
  published: new Date(),
  socials: [
    {
      name: 'twitter',
      url: 'https://twitter.com/openreplay'
    },
    {
      name: 'youtube',
      url: 'shorturl.at/insT6l'
    }
  ]
}

const copy = structuredClone(original) // 깊은 복사
original.socials[0].name = 'facebook' // 원본 수정

console.log(copy) // 원본 수정에 영향을 받지 않음
```

라이브러리나 복잡한 코드 없이 간단하게 사용 가능하며 대부분의 브라우저에서 지원된다.

#### structuredClone() vs JSON.parse(JSON.stringify(obj))

JSON.parse 방식은 `new Date()`와 같은 인스턴스를 객체로 복사하지 못하지만 structuredClone은 Date 객체를 복사할 수 있다.

```js
const Data = {
  date: new Date('2022-03-25')
}

const jsonCopy = JSON.parse(JSON.stringify(Data))
// {
//   date: "2022-03-25T00:00:00.000Z"
// }

const structuredCopy = structuredClone(Data)
// {
//   date: Object
// }
```

#### structuredClone()의 한계

- 함수는 복사할 수 없다.
- DOM 노드는 복사할 수 없다.
- 프로퍼티 디스크립터(Property descriptors), 세터(setter), 게터(getter)는 복사할 수 없다.
- 프로토타입 체인은 복제할 수 없다.

[(번역) StructuredClone API를 사용하여 객체를 깊은 복사하는 법](https://soobing.github.io/javascript/deep-copying-objects-with-the-structuredclone-api/#structuredclone-%EB%84%A4%EC%9D%B4%ED%8B%B0%EB%B8%8C-%ED%95%A8%EC%88%98%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%B4-%EA%B9%8A%EC%9D%80-%EB%B3%B5%EC%82%AC%ED%95%98%EA%B8%B0)<br/>
[structuredClone() 전역 함수](https://developer.mozilla.org/en-US/docs/Web/API/structuredClone#browser_compatibility)
