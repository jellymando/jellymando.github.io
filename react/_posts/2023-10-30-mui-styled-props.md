---
layout: post
title: '[MUI] Styled Component에 props 전달 시 에러'
sitemap: false
---

{:toc .large-only}

## 문제

MUI 라이브러리로 만든 스타일 컴포넌트에 props를 전달하면 아래와 같은 경고가 뜬다.

React does not recognize the `backgroundColor` prop on a DOM element. If you intentionally want it to appear in the DOM as a custom attribute, spell it as lowercase `backgroundcolor` instead. If you accidentally passed it from a parent component, remove it from the DOM element.

스타일 컴포넌트가 DOM element의 prop을 인식하지 못해서 발생하는 에러인 것 같다.

## 해결

MUI 공식문서에 나와있는 대로 shouldForwardProp 옵션을 전달해야 한다.

```js
const MyThemeComponent = styled('div', {
  shouldForwardProp: (prop) =>
    prop !== 'color' && prop !== 'variant' && prop !== 'sx'
})(({ theme }) => ({
  backgroundColor: 'aliceblue',
  padding: theme.spacing(1)
}))
```

`shouldForwardProp: (prop: string) => bool`

형식으로 옵션을 전달하고 props를 사용하면 된다!

## 참고사이트

[Custom components](https://mui.com/system/styled/#custom-components)
