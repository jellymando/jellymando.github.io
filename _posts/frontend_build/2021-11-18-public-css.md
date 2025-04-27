---
title: "public 경로의 css 파일 번들링하기"
categories: [FE Build]
tags: [webpack]
---

{:toc .large-only}

## webpack entry

`index.html` 에 link된 css 파일이 번들링되지 않아 고생했다.

webpack의 entry를 수정하면 원하는 파일을 추가하여 번들링할 수 있다.

entry의 프로퍼티 값을 배열로 설정할 수 있다는 걸 몰랐었다.

```js
module.exports = {
  //...
  entry: {
    main: ["./public/css/main.css", "./public/js/index.js"]
  }
};
```

참고로 배열 순서대로 번들링하기 때문에 global css 파일을 앞에 쓰지 않으면 global style 코드가 번들링 된 css 파일의 코드상 아래에 있게 된다.

## index.html 전/후

### public

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>까꿍</title>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
  </head>
  <body>
    <div id="root"></div>
  </body>
</html>
```

원래는 `index.html`에서 `src/index.js`를 링크했었지만 굳이 그럴 필요가 없다는 걸 깨닫고..

`index.js` 파일을 public/js/ 디렉토리로 이동했다.

### dist

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>까꿍</title>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <script defer src="js/build.js"></script>
    <link href="css/main.css" rel="stylesheet" />
  </head>
  <body>
    <div id="root"></div>
  </body>
</html>
```

public/ 경로 안의 `index.html`에는 css, js 모두 링크되지 않았지만 dist/ 경로 안의 `index.html`에는 번들링된 css와 js 파일이 링크된다.

## 디렉토리 수정

```js
└── dist
    ├── index.html
    ├── js
    │   ├── main.js
    └── css
        └── main.css
└── public
    ├── index.html
    ├── js
    │   ├── main.js
    └── css
        └── main.css
└── src
    ├── App.js
    ├── components
    │   ├── ...
    └── api
        └── ...
```

## 참고사이트

[Advanced entry](https://webpack.js.org/guides/entry-advanced/)
