---
layout: post
title: "[알고리즘] 정렬 알고리즘"
sitemap: false
---

{:toc .large-only}

## 정렬 알고리즘

배열을 순회하여 숫자를 정렬하는 알고리즘이다.

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

### 시간 복잡도

- 최선: O(n^2)
- 평균: O(n^2)
- 최악: O(n^2)

## 버블 정렬

- 배열을 2중 for문으로 순회하며 인접한 두 요소를 비교한다.
- 뒤에 있는 요소가 더 작으면 위치를 교환한다. (`[arr[j], arr[j + 1]] = [arr[j + 1], arr[j]]`)
- 이 과정을 통해 가장 큰 값이 마지막 인덱스로 이동하고, 그 다음 큰 값이 마지막 인덱스 앞부터 차례로 정렬된다.
- i 값이 커질때마다 마지막 인덱스부터 정렬되므로 안쪽 for문은 `let j = 0; j < arr.length - i - 1` 조건으로 순회한다.

```js
function bubbleSort(arr) {
  for (let i = 0; i < arr.length - 1; i++) {
    let sorted = true; //이미 정렬된 상태라고 가정

    for (let j = 0; j < arr.length - i - 1; j++) {
      if (arr[j] > arr[j + 1]) {
        [arr[j], arr[j + 1]] = [arr[j + 1], arr[j]];
        sorted = false; //swap 발생 = 미정렬 상태
      }
      if (sorted) break; // 이미 정렬된 상태이므로 종료
    }
  }
  return arr;
}
```

#### 시간 복잡도

- 최선: O(n) (배열이 이미 정렬된 경우)
- 평균: O(n^2)
- 최악: O(n^2)

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

### 시간 복잡도

- 최상: O(n) (배열이 이미 정렬된 경우)
- 평균: O(n^2)
- 최악: O(n^2)

## 퀵 정렬

- 피벗(pivot)을 기준으로 배열을 피벗보다 작은 배열과 피벗보다 큰 배열로 분할하고 이렇게 분할한 배열에 다시 퀵 정렬을 순환적으로 적용한다.
- 처음 피벗은 배열의 0번째 인덱스로 하며 분할함수에서 피벗의 인덱스를 리턴한다.
- 분할함수에서는 배열의 왼쪽과 오른쪽에서부터 피벗과 비교하면서 피벗보다 작은 요소를 발견하면 피벗의 index와 swap한다.
- 배열이 이미 정렬된 경우 배열이 2개로 분할되지 않으므로 최악의 시간 복잡도를 가진다.

```js
function swap(arr, i, j) {
  const temp = arr[i];
  arr[i] = arr[j];
  arr[j] = temp;
}

function partition(arr, left, right) {
  let pivot = arr[right];
  let pivotIdx = left;

  for (let i = left; i < right; i++) {
    if (arr[i] < pivot) {
      swap(arr, i, pivotIdx);
      pivotIdx++;
    }
  }
  swap(arr, pivotIdx, right);
  return pivotIdx;
}

function quickSort(arr, left = 0, right = arr.length - 1) {
  if (left < right) {
    const pivotIdx = partition(arr, left, right);
    quickSort(arr, left, pivotIdx - 1);
    quickSort(arr, pivotIdx + 1, right);
  }
  return arr;
}
```

### 시간 복잡도

- 최상: O(nlogn) (피벗 선택의 임의성이 보장된 경우)
- 평균: O(nlogn)
- 최악: O(n^2) (배열이 이미 정렬된 경우)

## 참고사이트

[삽입 정렬](https://www.zerocho.com/category/Algorithm/post/57e39fca76a7850015e6944a)<br>
[JavaScript로 Quick Sort(퀵 정렬) 구현하기](https://jun-choi-4928.medium.com/javascript%EB%A1%9C-quick-sort-%ED%80%B5-%EC%A0%95%EB%A0%AC-%EA%B5%AC%ED%98%84%ED%95%98%EA%B8%B0-76bf539abc0d)
