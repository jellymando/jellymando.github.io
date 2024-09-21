---
title: "텍스트 길어지면 말줄임표 처리하기✍️"
categories: [CSS]
tags: [css]
---

{:toc .large-only}

### 1줄 말줄임 처리하기

```css
.ellipsis {
  width: 100%;
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}
```

<br/>

- `text-overflow` : 이 속성은 글자가 지정한 너비를 넘어갈경우 어떤식으로 처리할 것인지를 선택하는 속성입니다.

  - `clip` : 기본값입니다.
  - `ellipsis` : **말줄임표로 처리합니다.** 상위요소의 너비가 auto로 되어있는경우는 적용할 수 없습니다.
  - `inherit` : 상위요소의 속성과 동일하게 사용합니다.

- `white-space` : 요소 안에서 공백은 어떤식으로 처리할것인지를 선택하는 속성입니다. 공백은 줄바꿈(line-break), 들여쓰기(tab), 공백(space)입니다.

  - `normal` : 기본값입니다. 공백을 여러개 넣어도 공백을 1개로 처리합니다.
  - `nowrap` : 공백을 여러개 넣어도 1개로 처리합니다. **텍스트가 길어져도 줄바꿈을 하지않고 1줄로 표시합니다.**
  - `pre` : 공백을 코드에 있는 그대로 표시합니다. 코드에 줄바꿈이 없으면 줄바꿈을 실행하지 않습니다.
  - `pre-wrap` : 공백을 코드에 있는 그대로 표시합니다. 코드에 줄바꿈이 없어도 자동으로 줄바꿈을 실행합니다. 코드에 줄바꿈이 있을때도 그대로 실행합니다.
  - `pre-line` : 공백을 여러개 넣어도 1개로 처리합니다. 코드에 줄바꿈이 없어도 자동으로 줄바꿈을 실행합니다. 코드에 줄바꿈이 있을때도 그대로 실행합니다.

> 기존에는 `word-wrap` 속성도 같이 사용했었는데, 현재는 `overflow-wrap`으로 이름이 다시 지어짐.([참고](https://developer.mozilla.org/ko/docs/Web/CSS/overflow-wrap)) `white-space: nowrap;` 만 사용해도 텍스트가 한 줄로 나오기 때문에 코드에서 뺌

### 2줄 이상 말줄임 처리하기

```css
.ellipsis {
  width: 200px;
  display: -webkit-box;
  overflow: hidden;
  text-overflow: ellipsis;
  -webkit-line-clamp: 2; /* 말줄임표 처리할 라인 수 */
  -webkit-box-orient: vertical;
  line-height: 1.4em;
  max-height: 2.8em;
}
```

<br/>

- `display: -webkit-box` : 해당 영역을 box 형태로 관리되도록 합니다.
- `-webkit-line-clamp` : 영역 내의 컨텐츠의 최대 라인수를 결정합니다.
- `-webkit-box-orient: vertical` : 영역 박스의 내의 정렬을 수직으로 하도록 합니다.
- `line-height`, `max-height` : `-webkit-line-clamp` 속성은 IE에서 적용되지 않기 때문에 `max-height`를 넘으면 말줄임표 처리

### 참고사이트

[CSS 말줄임 처리하기](https://blog.tjsrms.me/css-%EB%A7%90%EC%A4%84%EC%9E%84-%EC%B2%98%EB%A6%AC%ED%95%98%EA%B8%B0/)<br/>
[[HTML/CSS] 말줄임 표시 하는 방법: 1줄, 2줄 예제](https://deeplify.dev/front-end/markup/text-ellipsis#css-%EB%A7%90%EC%A4%84%EC%9E%84-2%EC%A4%84-%EC%9D%B4%EC%83%81-%EC%A0%81%EC%9A%A9%ED%95%98%EA%B8%B0)<br/>
[white-space](https://developer.mozilla.org/ko/docs/Web/CSS/white-space)
