---
layout: post
title: "React에서 이미지 파일 import 하기"
sitemap: false
---

{:toc .large-only}

```js
import { default as image } from "./image.jpg";
```

위와 같이 jpg 등의 이미지 파일을 import 하면 `모듈 또는 해당 형식 선언을 찾을 수 없습니다.` 에러 발생.

react-scripts 모듈을 인스톨해준다.

```js
yarn add react-scripts
```

src/ 경로 (index.js 경로?)에 `react-app-env.d.ts` 파일을 추가

```js
/* eslint-disable */
/// <reference types="react-scripts" />
```
