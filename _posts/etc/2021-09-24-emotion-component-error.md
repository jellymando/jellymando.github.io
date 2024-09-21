---
title: "[Emotion 에러] Component selectors can only be used in conjunction"
categories: [..etc]
tags: [emotion]
---

{:toc .large-only}

```js
export const Top = styled.div`
  ${Container} {
    border-bottom: 1px solid #d7d7d7;
  }
`;
```

Emotion으로 컴포넌트 스타일링 중 위와 같이 StyledComponent 코드 안에서 외부 컴포넌트를 참조하면 아래와 같은 에러가 뜬다.

`Component selectors can only be used in conjunction with @emotion/babel-plugin.`

아직 Emotion에서 외부 컴포넌트를 지원하지 않는 것 같다.

어쩔 수 없이 외부 컴포넌트를 인자로 전달하여 새로운 컴포넌트를 만들었다.

```js
export const HeaderContainer = styled(Container)`
  border-bottom: 1px solid #d7d7d7;
`;
```

<br/>

[Component selector error with Storybook/React/Typescript and Emotion](https://stackoverflow.com/questions/63677116/component-selector-error-with-storybook-react-typescript-and-emotion)
