---
layout: post
title: '[object-fit] 가로세로 비율 유지하면서 사이즈 조정하기'
sitemap: false
---

{:toc .large-only}

## 문제

이미지의 해상도에 상관없이 부모 요소의 가로와 세로를 꽉 채우게 하려고 한다.

```css
.parent {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100px;
  height: 100px;
}

.child {
  min-width: 100%;
  min-height: 100%;
}
```

위와 같이 css를 입히니 자식 요소의 가로가 세로보다 긴 경우 width가 100% 이상이 되는 게 아니라 100%가 되어버렸다.

`object-fit: cover`를 추가하면 요소의 기본 비율을 반드시 지키므로 자식 요소가 제대로 된 비율로 보이게 된다.

```css
.jasic {
  min-width: 100%;
  min-height: 100%;
  object-fit: cover;
}
```

## object-fit

#### object-fit: contain

콘텐츠의 기본 크기와 가로세로 비율을 유지하면서 부모 요소 가운데에 위치시킨다.

<img src="/assets/img/blog/2022-03-08-object-fit_01.png" style="margin: 30px 0">

#### object-fit: cover

콘텐츠의 가로세로 비율을 유지하면서 부모 요소를 가득 채운다.

부모와 가로세로 비율이 일치하지 않아서 밖으로 삐져나온 부분은 잘린다.

<img src="/assets/img/blog/2022-03-08-object-fit_02.png" style="margin: 30px 0">

#### object-fit: scale-down

콘텐츠의 기본 크기와 가로세로 비율을 유지하면서 `object-fit: none`과 `object-fit: contain` 중 더 <u>작은</u> 크기로 부모 요소 가운데에 위치시킨다.

부모 요소가 `video` 태그이고 `width: 100%; height: 100%` 속성일 때 `video[poster] {object-fit: contain}`을 적용한 경우,

처음 미디어를 불러올 때 `poster` 크기가 순간적으로 부모 사이즈에 맞춰 늘어났다가 contain 적용되는 경우가 있어 `object-fit: scale-down`을 적용했더니 정상적으로 노출되었다.

## 참고사이트

[[CSS] 이미지 사이즈 맞추기 (object-fit, absolute, background)](https://nykim.work/86)<br/>
[object-fit](https://developer.mozilla.org/ko/docs/Web/CSS/object-fit)
