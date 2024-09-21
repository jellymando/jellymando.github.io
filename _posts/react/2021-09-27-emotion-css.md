---
title: "[Emotion] css prop 사용 안되는 에러"
categories: [React]
tags: [emotion]
---

{:toc .large-only}

```js
// this comment tells babel to convert jsx to calls to a function called jsx instead of React.createElement
/** @jsx jsx */
import { css, jsx } from "@emotion/react";

const color = "darkgreen";

render(
  <div
    css={css`
      background-color: hotpink;
      &:hover {
        color: ${color};
      }
    `}
  >
    This has a hotpink background.
  </div>
);
```

코드상으로는 쉬워 보였는데 div의 css 속성에 빨간 밑줄이 그어지면서 css 속성을 사용할 수 없다는 typescript 에러가 발생한다.

Emotion 공식 문서를 확인해보면 css prop을 사용할 수 있는 방법으로는 Babel, JSX Pragma 두 가지가 있다.

- Babel

`.babelrc` 파일에

```js
{
  "presets": [
    [
      "@babel/preset-react",
      { "runtime": "automatic", "importSource": "@emotion/react" }
    ]
  ],
  "plugins": ["@emotion/babel-plugin"]
}
```

위 코드를 넣거나, `next.js`를 사용하는 경우 아래 코드를 넣는다.

```js
{
  "presets": [
    [
      "next/babel",
      {
        "preset-react": {
          "runtime": "automatic",
          "importSource": "@emotion/react"
        }
      }
    ]
  ],
  "plugins": ["@emotion/babel-plugin"]
}
```

<br/>

나는 위 방법으로 해결되지 않아서 (`next.js` 사용하는 프로젝트에서는 빨간 밑줄은 떠도 babel 만져주니까 정상적으로 돌아갔는데..) 두 번째 방법을 사용했다.

- jsx pragma

jsx pragma는 babel을 구성할 수 없는 프로젝트(create-react-app, codesandbox 등)에서 가장 잘 작동한다고 한다.

```js
/** @jsx jsx */
import { jsx } from "@emotion/react";
```

소스 파일의 맨 위에 jsx pragma를 설정하면 된다고 한다.

하지만 이로 인해 새로운 에러가 발생하였고.. (jsx 모듈 관련)

대신 아래 코드를 넣으니 잘 동작했다. 🙏

```js
/** @jsxImportSource @emotion/react */
import { jsx } from "@emotion/react";
```

Create React App 4 같은 new JSX runtimes 에서는 `/** @jsxImportSource @emotion/react */`를 사용해야 한다고 한다. (CRA는 안썼는데.. 어쨌든 해결돼서 다행이다..)

<br/>

[The css Prop](https://emotion.sh/docs/css-prop)<br/>
[JSX Pragma](https://emotion.sh/docs/css-prop#jsx-pragma)
