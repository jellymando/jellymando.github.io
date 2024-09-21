---
title: '[Vite] assets 빌드하기'
categories: [REACT]
tags: [vite]
---

{:toc .large-only}

## Vite로 assets 빌드하기

이미지 파일이 로컬에서는 잘 나오고 `npm run build` 시에도 dist 폴더에 잘 들어가지만, CI/CD 후에는 실제 서버에 배포되지 않아 파일 404 에러가 나서 찾아보다가..

이미지에 url('/assets/image.png') 이런 식으로 직접 경로를 입력하여서 에러남

```js
import imageUrl from '/assets/image.png' //src 폴더 안의 assets

return <img url={imageUrl} />
```

이미지를 import 해서 얻은 주소를 넣어주면 서버에도 잘 배포된다.. ㅠ

### Vite 공식 문서 참고

정적 에셋을 가져오게 되면 에셋에 접근할 수 있는 URL이 반환됩니다.

```js
import imgUrl from './img.png'
document.getElementById('hero-img').src = imgUrl
```

예를 들어, imgUrl 객체는 개발 시 /img.png 값으로 할당되겠으나, 실제 프로덕션 버전에서는 /assets/img.2d8efhg.png와 같은 값이 할당됩니다. (여기서 2d8efhg는 해시 값을 의미합니다. - 옮긴이)

## 참고사이트

[URL을 통해 에셋 가져오기](https://ko.vitejs.dev/guide/assets.html#importing-asset-as-url)
