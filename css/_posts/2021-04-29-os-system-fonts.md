---
layout: post
title: "OS별 기본 시스템 폰트 정리"
sitemap: false
---

{:toc .large-only}

### OS별 시스템 폰트

| OS       |              Version               |          System Font |
| -------- | :--------------------------------: | -------------------: |
| Mac OS X |             El Capitan             |        San Francisco |
| Mac OS X |              Yosemite              |       Helvetica Neue |
| Mac OS X |             Mavericks              |        Lucida Grande |
| Windows  |               Vista                |             Segoe UI |
| Windows  |                 XP                 |               Tahoma |
| Windows  |             3.1 to ME              | Microsoft Sans Serif |
| Android  |     Ice Cream Sandwich (4.0)+      |               Roboto |
| Android  | Cupcake (1.5) to Honeycomb (3.2.6) |           Droid Sans |
| Ubuntu   |            All versions            |               Ubuntu |

### css에 적용하기

```css
body {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica,
    Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol";
}
```

[System Font Stack](https://css-tricks.com/snippets/css/system-font-stack/)
