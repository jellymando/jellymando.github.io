---
title: "[알고리즘] 조합과 순열로 경우의 수 구하기"
date: 2025-03-07T00:00:00+09:00
categories: [Algorithm]
tags: [algorithm, 조합, 순열]
---

{:toc .large-only}

## 조합과 순열

- 길이가 l인 배열에서 n개의 요소를 선택하는 알고리즘
- 재귀함수를 통해 만들 수 있는 경우의 수(배열)를 모두 생성한다.

## 조합 (Combination)

- 배열을 만들 때 현재 요소를 포함시키지 않는다.
- 자신의 index보다 큰 배열을 재귀 함수에 전달한다.
- `[3,6]`과 `[6,3]`을 동일한 원소로 판단한다. 즉 순서를 고려하지 않는다.
- ex) `permutation([3,6,9], 2)` => [ [ 3, 6 ], [ 3, 9 ], [ 6, 9 ] ]

<img src="/assets/img/blog/2024-03-07-combination.png" style="margin:10px 0;">

```js
function combination(array, selectNum, result = []) {
  if (selectNum === 1) return arr.map((v) => [v]);

  arr.forEach((item, i) => {
    const perArr = permutation(
      arr.filter((item, idx) => idx > i),
      selectNum - 1,
      result
    );
    result.push(...perArr.map((v) => [item, ...v]));
  });

  return result;
}
```

1. `combination([3,6,9], 2)`가 호출된다.
1. `arr.forEach`에서 [3,6,9]를 순회한다.
1. `arr.filter`에서 index가 0보다 큰 배열 [6,9]와 1을 재귀 함수로 전달한다.
1. `combination([6,9], 1)`가 호출된다.
1. `if (selectNum === 1)` 조건문이 참이 되어 [ [ 6 ], [ 9 ] ]를 리턴한다.
1. 3번 스택(item=3, i=0)으로 돌아와서 다음 줄을 실행한다.
1. [3,6], [3,9]를 result에 push한다.
1. `arr.forEach`에서 다음 인덱스를 순회한다.

### 중복조합

- 배열을 만들 때 현재 요소를 포함시킨다.
- 자신의 index보다 같거나 큰 배열을 재귀 함수에 전달한다.
- ex) `permutation([3,6,9], 2)` => [
  [ 3, 3 ],
  [ 3, 6 ],
  [ 3, 9 ],
  [ 6, 6 ],
  [ 6, 9 ],
  [ 9, 9 ]
  ]

```js
function permutation(arr, selectNum, result = []) {
  if (selectNum === 1) return arr.map((v) => [v]);

  arr.forEach((item, i) => {
    const perArr = permutation(
      arr.filter((item, idx) => idx >= i),
      selectNum - 1,
      result
    );
    result.push(...perArr.map((v) => [item, ...v]));
  });

  return result;
}
```

## 순열 (Permutation)

- 배열을 만들 때 현재 요소를 포함시키지 않는다.
- 자신의 index를 제외한 배열을 재귀 함수에 전달한다.
- `[3,6]`과 `[6,3]`을 동일하지 않은 원소로 판단한다. 즉 순서를 고려한다.
- ex) `permutation([3,6,9], 2)` => [
  [ 3, 6 ],
  [ 3, 9 ],
  [ 6, 3 ],
  [ 6, 9 ],
  [ 9, 3 ],
  [ 9, 6 ]
  ]

<img src="/assets/img/blog/2024-03-07-permutation.png" style="margin:20px 0;">

```js
function permutation(arr, selectNum, result) {
  if (selectNum === 1) return arr.map((v) => [v]);

  arr.forEach((item, i) => {
    const perArr = permutation(
      arr.filter((item, idx) => idx !== i),
      selectNum - 1,
      result
    );
    result.push(...perArr.map((v) => [item, ...v]));
  });

  return result;
}
```

1. `permutation([3,6,9], 2)`가 호출된다.
1. `arr.forEach`에서 [3,6,9]를 순회한다.
1. `arr.filter`에서 index 0을 제외한 나머지 배열 [6,9]와 1을 재귀 함수로 전달한다.
1. `permutation([6,9], 1)`가 호출된다.
1. `if (selectNum === 1)` 조건문이 참이 되어 [ [ 6 ], [ 9 ] ]를 리턴한다.
1. 3번 스택(item=3, i=0)으로 돌아와서 다음 줄을 실행한다.
1. [3,6], [3,9]를 result에 push한다.
1. `arr.forEach`에서 다음 인덱스를 순회한다.

### 중복순열

- 배열을 만들 때 현재 요소를 포함시킨다.
- 자신의 index를 포함한 배열을 재귀 함수에 전달한다.
- ex) `permutation([3,6,9], 2)` => [
  [ 3, 3 ], [ 3, 6 ],
  [ 3, 9 ], [ 6, 3 ],
  [ 6, 6 ], [ 6, 9 ],
  [ 9, 3 ], [ 9, 6 ],
  [ 9, 9 ]
  ]

```js
function permutation(arr, selectNum, result) {
  if (selectNum === 1) return arr.map((v) => [v]);

  arr.forEach((item, i) => {
    const perArr = permutation(arr, selectNum - 1, result);
    result.push(...perArr.map((v) => [item, ...v]));
  });

  return result;
}
```

### swap 방식

- 순열을 구하는 다른 방법 중 원본 배열의 요소들의 위치를 교환해주며 경우의 수를 구하는 swap 방식도 있다.
- filter, map 등으로 배열을 새로 생성하지 않고 원본 배열의 순서만 바꾸므로 공간복잡도는 작지만 순열의 순서를 보장하지는 않는다.

```js
function permutation(arr, selectNum, idx = 0, result = []) {
  if (idx === selectNum) return result.push(arr);

  function swap(i, j) {
    [arr[i], arr[j]] = [arr[j], arr[i]];
  }

  arr.forEach((item, i) => {
    swap(idx, i);
    permutation(arr, selectNum, idx + 1, result);
    swap(i, idx);
  });

  return result;
}
```

1. `permutation([3,6,9], 2)`가 호출된다.
1. `arr.forEach`에서 [3,6,9]를 순회한다.
1. `swap(0,0)` 호출 -> i,j 값이 같아 arr 배열에 변화가 없다.
1. `permutation([3,6,9], 2, 1, [])`이 호출된다.
1. `arr.forEach`에서 [3,6,9]를 순회한다.
1. `swap(1,0)` 호출 -> arr[1]과 arr[0]의 순서가 교환된다. ([6,3,9])
1. `permutation([6,3,9], 2, 2, [])`이 호출된다.
1. `if (selectNum === 1)` 조건문이 참이 되어 result에 [6, 3, 9]를 push한다.
1. 4번 스택(item=3, i=0)으로 돌아와서 다음 줄을 실행한다.
1. `swap(0,1)` 호출 -> arr[0]과 arr[1]의 순서가 교환된다. ([3,6,9])
1. `arr.forEach`에서 다음 인덱스를 순회한다. (item=6, i=1)
1. `swap(1,1)` 호출 -> i,j 값이 같아 arr 배열에 변화가 없다.
1. `permutation([3,6,9], 2, 2, [])`이 호출된다.
1. `if (selectNum === 1)` 조건문이 참이 되어 result에 [3,6,9]를 push한다.
1. `swap(1,1)` 호출 -> i,j 값이 같아 arr 배열에 변화가 없다.
1. `arr.forEach`에서 다음 인덱스를 순회한다. (item=9, i=2)

## 참고사이트

[[JS] 순열 / 중복순열 / 조합 / 중복조합](https://8ugust-dev.tistory.com/46)<br/>
[[javascript] 순열, 조합, 중복순열, 중복조합](https://jjnooys.medium.com/javascript-%EC%88%9C%EC%97%B4-%EC%A1%B0%ED%95%A9-%EC%A4%91%EB%B3%B5%EC%88%9C%EC%97%B4-%EC%A4%91%EB%B3%B5%EC%A1%B0%ED%95%A9-ced4d4c868bf)<br/>
[조합과 순열](https://huimang2.github.io/algorithm/combination_permutation.html)
