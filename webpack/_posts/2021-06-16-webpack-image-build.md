---
layout: post
title: "[url-loader] 이미지 파일 base64 URL로 변환하기"
sitemap: false
---

{:toc .large-only}

npm 라이브러리를 만들었지만 이미지 파일을 라이브러리에 빌드하는 방법을 찾지 못했다..

`/node_modules/내라이브러리/` 경로에 이미지 폴더가 생성되지 않는다.

그래서 `file-loader`가 아닌 `url-loader`를 사용하게 되었다.

`file-loader`는 파일을 build 폴더에 생성시켜주는 역할을 한다.

public 혹은 src 폴더의 이미지 파일을 build 파일에 복사하는 것과 같다.

`url-loader`는 파일을 복사하지 않고 base64 URL로 변환한다.

예시 : `data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAEAAAABACAYAAACqaXHeAAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAABuwAAAbsBOuzj4gAAABl0RVh0U29mdHdhcmUAd3d3Lmlua3NjYXBlLm9yZ5vuPBoAAAatSURBVHic5Zp7bFvVHcc/P9/ra+fRR1KakocLzdIkTR...`

`webpack.config.js` 파일을 수정해준다.

```js
module.exports = {
  module: {
    rules: [
      {
        test: /\.(png|jpg|gif)$/i,
        use: [
          {
            loader: "url-loader",
            options: {
              limit: 8192,
            },
          },
        ],
      },
    ],
  },
};
```

`options.limit`는 limit보다 작은 파일만을 변환하도록 설정하는 값이다.

위와 같이 웹팩을 수정하니 실제 라이브러리를 사용하는 프로젝트에서도 정상적으로 이미지 출력되었다..

<br/>

[file-loader vs url-loader](https://velog.io/@jeongnaehyeok/file-loader-vs-url-loader)<br/>
[url-loader](https://v4.webpack.js.org/loaders/url-loader/)
