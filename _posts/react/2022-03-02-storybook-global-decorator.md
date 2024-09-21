---
title: "[Storybook] Global decorators - 공통 스타일 적용하기"
categories: [REACT]
tags: [storybook]
---

{:toc .large-only}

## Global decorators

storybook 템플릿에 직접 `<Global />` 코드를 넣자 에러가 발생했다.

Global Style을 적용하려면 Global decorators를 설정해야 한다.

`.storybook/preview.js` 파일에 아래 코드를 추가한다.

```js
import { Global } from "@emotion/react";
import { Reset } from "styles";

export const decorators = [
  (Story) => (
    <>
      <Global styles={Reset} />
      <Story />
    </>
  )
];
```

## Component decorators

컴포넌트 단위로 넣으려면 컴포넌트의 stories 파일에 아래와 같이 추가한다.

```js
// Button.stories.js|jsx

import React from "react";

import { Button } from "./Button";

export default {
  title: "Button",
  component: Button,
  decorators: [
    (Story) => (
      <>
        <Global styles={Reset} />
        <Story />
      </>
    )
  ]
};
```

## 참고사이트

[Global decorators](https://storybook.js.org/docs/react/writing-stories/decorators#global-decorators)
