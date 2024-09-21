---
title: "[VSCode] 에디터 폰트 변경, 줄간격 변경하기"
categories: [ETC]
tags: [vscode]
---

{:toc .large-only}

### 폰트 변경

`File > Preperences > Settings` 혹은 `Ctrl + ,`

<img src="/assets/img/blog/2021-08-17-vscode-editor-font.png"/>

<br/>

한국어 기준으로 `텍스트 편집기 > 글꼴` 항목에서 폰트 수정

### 줄간격 변경

`settings.json` 파일에 원하는 lineHeight 추가

```js
"editor.lineHeight": 19,
```

<br/>

[[VSCode] 터미널 폰트, 글자 크기 변경하기](https://hianna.tistory.com/350)
