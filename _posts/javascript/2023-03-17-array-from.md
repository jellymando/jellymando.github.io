---
title: 'read only 속성의 객체를 writeable로 복사하는 방법'
categories: [Javascript]
tags: [javascript]
---

{:toc .large-only}

## read only 속성의 객체를 writeable로 복사하는 방법

```js
const readOnlyObj = {
  prop1: 'value1',
  prop2: 'value2'
}

// Object.assign()을 사용하여 객체 복사
const writableCopy = Object.assign({}, { ...readOnlyObj })

// writableCopy에서 속성 값을 변경
writableCopy.prop1 = 'new value'

console.log(readOnlyObj.prop1) // 'value1'
console.log(writableCopy.prop1) // 'new value'
```

`Object.assign()` 메서드에 첫 번째 인자로 빈 객체를 전달하고, 두 번째 인자로 원본 객체를 스프레드 연산자로 복사한다.

이렇게 생성된 writableCopy 객체는 readOnlyObj 객체와 동일한 속성 및 값을 갖지만 수정할 수 있는 별도의 쓰기 가능한 객체가 된다.

## read only 속성의 객체들로 이루어진 배열을 writeable로 복사하는 방법

```js
const readOnlyArray = [
  { name: 'Alice', age: 30 },
  { name: 'Bob', age: 40 }
]
const writeableArray = Array.from(readOnlyArray, (obj) => ({ ...obj }))

writeableArray[0].age = 35

console.log(readOnlyArray[0].age) // 30
console.log(writeableArray[0].age) // 35
```

`Array.from()` 메서드에 첫 번째 인자로 원본 배열을 전달하고, 두 번째 인자로 객체를 복사하는 콜백 함수를 전달한다.

콜백 함수에서 객체를 스프레드 연산자로 복사한다.

이렇게 생성된 새로운 배열은 원본 배열과는 별개의 객체이므로, 원본 배열을 수정해도 영향을 받지 않는다.
