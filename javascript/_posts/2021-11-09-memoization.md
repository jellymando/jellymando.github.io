---
layout: post
title: "메모이제이션(Memoization) 사용하기"
sitemap: false
---

{:toc .large-only}

## 메모이제이션

메모이제이션은 함수의 호출 결과를 저장하고 동일한 입력이 다시 제공될 때 **캐시된 결과를 반환**하여 실행 속도를 높이는 최적화 방법이다.

주로 재귀 함수와 클로저 기법을 사용해 동작한다.

## 예시 : 피보나치 수열

```js
const fibonacci = (num) => {
  if (num < 2) {
    return num;
  } else {
    return fibonacci(num - 1) + fibonacci(num - 2);
  }
};
fibonacci(5);
```

재귀함수를 이용한 피보나치 수열 함수를 메모이제이션을 사용해 최적화 해보자.

```js
const fibonacci = (function () {
  const memo = {};
  const fibo = (num) => {
    if (num < 2) {
      return num;
    } else {
      const memo1 = memo[num - 1] || fibo(num - 1);
      const memo2 = memo[num - 2] || fibo(num - 2);
      const result = memo1 + memo2;
      console.log(memo1, memo2, result);
      memo[num] = result;
      return result;
    }
  };
  return fibo;
})();

fibonacci(5); // 1 0 1, 1 1 2, 2 1 3, 3 2 5, 5
fibonacci(5); // 3 2 5, 5
```

콘솔을 찍어보면 처음 호출했을 때는 메모이제이션 된 값이 없어 재귀함수가 실행되지만, 같은 값을 다시 호출했을 때는 메모이제이션 된 값을 가져와 한번만에 값을 반환한다.

## 원리

fibonacci 함수는 즉시 실행 함수이기 때문에 실행된 후 **클로저**가 된다.

> 클로저 : 생명주기가 끝났어도 외부 함수에 의해 참조되는 함수. 브라우저의 가비지 컬렉터는 생명주기가 끝났어도 참조되고 있는 함수는 제거하지 않는다.

fibonacci 함수를 실행하면 fibo 함수가 return되며, memo 객체는 초기화되지 않고 유지되며 새로운 num으로 호출될 때마다 값이 추가된다.

## 참고사이트

[재귀(recursion)와 메모이제이션(Memoization)](https://www.zerocho.com/category/JavaScript/post/579248728241b6f43951af19)<br/>
[[번역] 자바스크립트 메모이제이션](https://www.devh.kr/2020/Understanding-Memoization-In-JavaScript/#What-is-memoization)
