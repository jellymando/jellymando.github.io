---
title: 'SVG 커스텀 함수 만들기 (fill, width, height 옵션)'
categories: [HTML]
tags: [svg]
---

{:toc .large-only}

## SVG 커스텀 함수 만들기

기본적인 svg 엘리먼트의 html 코드는 아래와 같다.

```html
<svg
  width="300"
  height="300"
  viewBox="0 0 300 300"
  xmlns="http://www.w3.org/2000/svg"
  stroke="red"
  fill="grey"
></svg>
```

svg를 리턴하는 함수를 만들어서 사용할 수 있다.

```js
const svg = () => `
<svg
  width="300"
  height="300"
  viewBox="0 0 300 300"
  xmlns="http://www.w3.org/2000/svg"
  stroke="red"
  fill="grey"
></svg>
`
export default svg
```

svg를 커스텀하기 위해 파라미터값을 추가한다.

크기를 설정하려면 width, height 값을 수정하고, **viewBox 값은 수정하지 않아도 된다.**

viewBox를 수정하면 좌표까지 변경되어 버린다.

```js
const svg = ({ width = "300", height = "300", fill ="grey" }) => `
<svg
  width="${width}"
  height="${height}"
  viewBox="0 0 300 300"
  xmlns="http://www.w3.org/2000/svg"
  stroke="red"
  fill="${fill}"
></svg>
```

## 참고사이트

[How to Scale SVG to Fit within a Certain Size (without distorting the image)](https://css-tricks.com/scale-svg/#aa-how-to-scale-svg-to-fit-within-a-certain-size-without-distorting-the-image)
