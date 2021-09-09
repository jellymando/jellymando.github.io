---
layout: post
title: "inline과 inline-block의 차이, 여백 없애기"
sitemap: false
---

{:toc .large-only}

## inline

- text 크기만큼만 점유한다.
- width와 height를 지정할 수 없다.
- <u>padding, margin을 지정하면 시각적으로는 적용되지만, height 공간을 점유하지 못한다.</u>
  - padding을 사용하여 height가 100px인 것처럼 나와도, 부모의 height에 영향을 주지 못한다.
  - 공간을 점유하지 못해 상하 요소와 겹침이 발생한다.
- line-height를 적용할 수 없다. (부모 요소에 적용됨)

## inline-block

- text 크기만큼만 점유한다.
- width와 height를 지정할 수 있다.
- padding, margin을 지정하면 공간을 점유한다.
- 요소간 margin과 별개로 여백이 발생한다.

## inline 요소의 여백 없애기

- 공백 제거
  - 엘리먼트들을 줄바꿈하지 않고 사용하거나
  - `<span><!--/n--><span>` 사용
- 폰트 사이즈 조정
  - 부모 요소에 `font-size: 0` 적용
- margin 속성 조정
  - 요소에 `margin-right: -4px;` 적용
- float 속성 사용
  - 부모 요소에 `float: left;` 적용
- flex 속성 사용
  - 부모 요소에 `display: flex;` 적용

## 참고사이트

[[CSS] display - block과 inline 그리고 inline-block](https://seungwoohong.tistory.com/23)<br/>
[[CSS] inline 속성일 때, 4px의 여백에 대하여](https://norux.me/63)
