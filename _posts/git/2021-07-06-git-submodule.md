---
title: "git에 저장된 repository를 module로 사용하기"
categories: [Git]
tags: [git]
---

{:toc .large-only}

### git에 저장된 repository를 module로 사용하기

## npm install

```js
npm install git+https://github.com/visionmedia/express.git
// 혹은
npm install git+ssh://git@github.com/visionmedia/express.git
```

<br/>

package.json에 모듈이 추가된 것을 확인할 수 있다.

<br/>

[How to install an npm package from GitHub directly?](https://stackoverflow.com/questions/17509669/how-to-install-an-npm-package-from-github-directly)
