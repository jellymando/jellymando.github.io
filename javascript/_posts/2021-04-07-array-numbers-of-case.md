---
layout: post
title: '배열을 조합하여 만들 수 있는 모든 배열 구하기'
sitemap: false
---

{:toc .large-only}

### 알고리즘

재귀 함수를 이용하여 배열을 조합하여 만들 수 있는 모든 배열 구하기

```js
let answer = [];
const combination = (nums, num, j = 0, arr = []) => {
  if (j === num) answer.push([...arr]);
  else {
    for (let i = 0; i < nums.length; i++) {
      arr.push(nums[i]);
      combination(nums.slice(i + 1), num, j + 1, arr);
      arr.pop();
    }
  }
};
combination([1, 2, 3, 4], 3);
```
