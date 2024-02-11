---
layout: post
title: "[정렬 알고리즘] 선택정렬, 버블정렬, 삽입정렬"
sitemap: false
---

{:toc .large-only}

## 정렬 알고리즘

배열을 순회하여 숫자를 오름차순 혹은 내림차순으로 정렬한다.

배열을 정렬하는 방법에는 선택정렬, 버블정렬, 삽입정렬 등이 있다.

아래 정렬들은 오름차순 기준으로 설명한다.

## 선택 정렬

- 배열을 2중 for문으로 순회하며 `arr[minIndex]`보다 작은 최소값 index을 찾는다. minIndex의 초기값은 i이다.
- 최소값을 찾은 후 현재 요소와 배열 순서를 교환한다. (ex. `[arr[j], arr[minIndex]] = [arr[minIndex], arr[j]]`)
- 이 과정을 통해 가장 작은 값이 첫 번째 인덱스로 이동하고, 그 다음 작은 값이 첫 번째 인덱스 뒤부터 차례로 정렬된다.
- i 값이 커질때마다 첫 번째 인덱스부터 정렬되므로 안쪽 for문은 `let j = i + 1; j < arr.length;` 조건으로 순회한다.

```js
function selectionSort(arr) {
  for (let i = 0; i < arr.length - 1; i++) {
    let minIndex = i;
    for (let j = i + 1; j < arr.length; j++) {
      if (arr[j] < arr[minIndex]) {
        minIndex = j;
      }
    }
    if (minIndex !== i) {
      [arr[i], arr[minIndex]] = [arr[minIndex], arr[i]];
    }
  }
  return arr;
}
```

## 버블 정렬

- 배열을 2중 for문으로 순회하며 인접한 두 요소를 비교한다.
- 뒤에 있는 요소가 더 작으면 위치를 교환한다. (`[arr[j], arr[j + 1]] = [arr[j + 1], arr[j]]`)
- 이 과정을 통해 가장 큰 값이 마지막 인덱스로 이동하고, 그 다음 큰 값이 마지막 인덱스 앞부터 차례로 정렬된다.
- i 값이 커질때마다 마지막 인덱스부터 정렬되므로 안쪽 for문은 `let j = 0; j < arr.length - i - 1` 조건으로 순회한다.

```js
function bubbleSort(arr) {
  for (let i = 0; i < arr.length - 1; i++) {
    for (let j = 0; j < arr.length - i - 1; j++) {
      if (arr[j] > arr[j + 1]) {
        [arr[j], arr[j + 1]] = [arr[j + 1], arr[j]];
      }
    }
  }
  return arr;
}
```

## 삽입 정렬

- 배열을 2중 for문으로 순회하며 i는 1 인덱스부터 시작하여 점점 커지고, j는 i-1부터 시작하여 점점 작아진다.
- 변수 j의 스코프는 for문 바깥에 있다. 그래서 for문이 break 되지 않고 전부 순환되어 끝나면 j의 값은 -1이 된다.
- arr[j]와 tmp 값을 비교하여 arr[j] 값이 더 크면 j+1 인덱스에 arr[j]를 삽입한다.
- arr[j]와 tmp 값을 비교하여 arr[j] 값이 더 크지 않으면 break한다.
- for문이 끝나면 마지막 j+1 인덱스에 tmp를 삽입한다.
- 안쪽 for문에 `arr[j] > tmp` 조건을 붙이면 배열이 이미 정렬된 경우 시간복잡도를 최적화 할 수 있다.

```js
function insertionSort(arr) {
  for (let i = 1; i < arr.length; i++) {
    let tmp = arr[i];
    let j;
    for (j = i - 1; j >= 0 && arr[j] > tmp; j--) {
      arr[j + 1] = arr[j];
    }
    arr[j + 1] = tmp;
  }
  return arr;
}
```

## 시간 복잡도

#### 선택 정렬

- 최선: O(n^2)
- 평균: O(n^2)
- 최악: O(n^2)

#### 버블 정렬

- 최선: O(n^2)
- 평균: O(n^2)
- 최악: O(n^2)

#### 삽입 정렬

- 최상: O(n) (배열이 이미 정렬된 경우)
- 평균: O(n^2)
- 최악: O(n^2)

세 가지 정렬 알고리즘 모두 최악의 경우 O(n^2)의 시간 복잡도를 가지므로 대규모 데이터 세트에 대해 비효율적이다.

삽입 정렬은 배열이 이미 정렬된 경우 조건문으로 O(n)의 시간 복잡도를 최적화할 수 있지만 선택 정렬, 버블 정렬은 항상 동일한 시간 복잡도가 걸린다.

더 큰 배열의 경우 병합 정렬, 빠른 정렬 또는 힙 정렬과 같은 다른 보다 효율적인 정렬 알고리즘을 사용하는 것이 좋다.

## 참고사이트

[삽입 정렬](https://www.zerocho.com/category/Algorithm/post/57e39fca76a7850015e6944a)
