---
title: "styled-components에서 for문 돌리기"
categories: [React]
tags: [react, styled components]
---

{:toc .large-only}

`styled-components`에서 각 엘리먼트에 animation을 적용하려다 `for`문 코드에 대해 알아보았다.

```js
const createCSS = () => {
  let str = "";
  for (let i = 1; i < 30; i++) {
    str += `
            &:nth-of-type(${i}) {
                transform: translate3d(${random(190) - 100}px, ${
      random(200) - 100
    }px, 0) rotate(${random(360)}deg);
                background: hsla(${random(360)}, 100%, 50%, 1);
            }
        `;
  }
  return str;
};

export const Container = styled.div`
  ${I} {
    ${createCSS()}
    animation: ${bang} 700ms ease-out forwards;
  }
`;
```

<br/>

`for`문을 포함한 함수를 따로 만들어서 `return` 시켜야 한다.

`for`문 안에서는 animation css를 작성하면 에러가 나므로 빠로 빼주어야 한다.

<br/>

[@for loops in styled-components](https://stackoverflow.com/questions/52696511/for-loops-in-styled-components)<br/>
[Loop nth-child in styled component](https://spectrum.chat/styled-components/general/loop-nth-child-in-styled-component~7342bb0f-0fb6-4548-ac56-75834008af69)
