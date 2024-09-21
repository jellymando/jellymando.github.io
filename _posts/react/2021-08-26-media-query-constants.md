---
title: "Media Query 변수화해서 Styled-Components에서 사용하기"
categories: [REACT]
tags: [react, media query]
---

{:toc .large-only}

### 변수 선언

```js
export const MEDIA = {
  MOBILE: (css: string) => {
    return `@media screen and (max-width: 600px) {
                ${css}
            }`;
  },
  TABLET: (css: string) => {
    return `@media screen and (max-width: 1024px) {
                ${css}
            }`;
  },
};
```

### Styled-Components 내에서 사용

```js
    ${MEDIA.TABLET(`
        font-size: ${FONTSIZE.MIDDLE};
    `)};

    ${MEDIA.MOBILE(`
        font-size: ${FONTSIZE.SMALL};
    `)};
```
