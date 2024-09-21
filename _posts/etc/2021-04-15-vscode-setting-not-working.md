---
title: "VSCode setting 적용 안될 때"
categories: [ETC]
tags: [vscode]
---

{:toc .large-only}

```js
{
    // Set the default
    "editor.formatOnSave": false,
    // Enable per-language
    "[javascript]": {
        "editor.formatOnSave": true
    },
    "editor.codeActionsOnSave": {
        // For ESLint
        "source.fixAll.eslint": true
    },
    "editor.defaultFormatter": "esbenp.prettier-vscode"
}
```

VSCode에서 파일 저장 시 자동으로 format 되도록 setting 파일을 수정했지만 적용되지 않는다.

`command + ,` 로 설정에 들어가서 default formatter를 검색하고 기본 포맷터를 Prettier로 설정한다.

혹은 setting.json 에 아래와 같이 추가해도 될 것 같다.

```js
"editor.defaultFormatter": "esbenp.prettier-vscode"
```
