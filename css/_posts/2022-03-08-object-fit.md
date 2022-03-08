---
layout: post
title: '[object-fit] 가로세로 비율 유지하면서 사이즈 조정하기'
sitemap: false
---

{:toc .large-only}

## 문제

이미지의 해상도에 상관없이 부모 요소의 가로와 세로를 꽉 채우게 하려고 한다.

```css
.bumo {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100px;
  height: 100px;
}
.jasic {
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

대체 콘텐츠의 가로세로비를 유지하면서, 요소의 콘텐츠 박스 내부에 들어가도록 크기를 맞춤 조절합니다.

콘텐츠가 콘텐츠 박스 크기에 맞도록 하면서도 가로세로비를 유지하게 되므로, 서로의 가로세로비가 일치하지 않으면 객체가 "레터박스"처럼 됩니다.

<img src="/assets/img/blog/2022-03-08-object-fit_01.png" style="margin: 30px 0">

#### object-fit: cover

대체 콘텐츠의 가로세로비를 유지하면서, 요소 콘텐츠 박스를 가득 채웁니다.

서로의 가로세로비가 일치하지 않으면 객체 일부가 잘려나갑니다.

<img src="/assets/img/blog/2022-03-08-object-fit_02.png" style="margin: 30px 0">

## 참고사이트

[[CSS] 이미지 사이즈 맞추기 (object-fit, absolute, background)](https://nykim.work/86)<br/>
[object-fit](https://developer.mozilla.org/ko/docs/Web/CSS/object-fit)
