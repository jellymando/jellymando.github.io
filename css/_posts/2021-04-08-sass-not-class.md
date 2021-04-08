---
layout: post
title: "SCSS 특정 클래스를 포함했는지 감지하여 스타일 적용하기"
sitemap: false
---

{:toc .large-only}

스타일 속성에서 `&:not()` 사용

```css
[class*='icon-'] {
        margin: 0;
        &:not(.black) {
            color: $white;
        }
    }
    ~~~
```
