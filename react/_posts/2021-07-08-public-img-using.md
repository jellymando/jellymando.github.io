---
layout: post
title: "CRA로 만든 리액트 프로젝트에서 public 폴더 이미지 사용하기"
sitemap: false
---

{:toc .large-only}

### CRA로 만든 리액트 앱은 src 경로 밖에 접근할 수 없다.

때문에 `import`를 통해 public 폴더에 접근하기 어렵다.

src 폴더 안에 이미지 파일을 넣으면 되지만 구조적으로 마음에 들지 않는다.

### public 폴더 안에 img 폴더를 만들고 이미지 파일을 넣는다.

import 대신 `background-image`나 `img src=""`를 사용하기로 한다.

경로가 `public/img/image.png`면

```html
<img src="/img/image.png" />
```

<br/>

```css
background-image: url("img/image.png");
```

<br/>

두 방법으로 이미지를 가져올 수 있다.

[React 프로젝트에서 이미지 import하는 방법](https://writingdeveloper.blog/301)
