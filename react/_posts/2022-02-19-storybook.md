---
layout: post
title: 'Storybook을 사용한 design-system 만들기'
sitemap: false
---

{:toc .large-only}

## Storybook 설치

```bash
npm i storybook@latest --save-dev init
```

`package.json`에 아래와 같은 CLI가 생기며, `.storybook` 폴더가 생성된다.

```js
  "scripts": {
    // ...
    "storybook": "storybook dev -p 6006",
    "build-storybook": "storybook build"
  }
```

## Webpack 설정

Storybook에서 컴포넌트를 import할 때 절대경로를 사용한다면 웹팩을 설정해주어야 한다.

.storybook 폴더에 webpack.config.js 파일을 생성하고 아래 코드를 저장한다.

```js
const path = require('path')

module.exports = ({ config }) => {
  config.resolve.modules.push(path.resolve(__dirname, '../src'))
  return config
}
```

## addon 탭 만들기

<img src="/assets/img/blog/2023-06-27-storybook_01.png" style="margin-bottom:30px;">

storybook 플러그인을 추가하여 하단 탭을 만들 수 있다.

```bash
npm i @storybook/manager-api @storybook/components --save-dev
```

.storybook 폴더에 preset.js 파일을 생성한다.

```js
// preset.js
function managerEntries(entry = []) {
  return [...entry, require.resolve('./manager')] //👈 Addon implementation
}

export default { managerEntries }
```

같은 경로에 manager.js 파일을 생성한다.

```js
import React from 'react'
import { addons, types } from '@storybook/manager-api'
import { AddonPanel } from '@storybook/components'

const ADDON_ID = 'myaddon'
const PANEL_ID = `${ADDON_ID}/panel`

// give a unique name for the panel
const MyPanel = () => <div>MyAddon</div>

addons.register(ADDON_ID, (api) => {
  addons.add(PANEL_ID, {
    type: types.PANEL,
    title: 'My Addon',
    render: ({ active, key }) => (
      <AddonPanel active={active} key={key}>
        <MyPanel />
      </AddonPanel>
    )
  })
})
```

.storybook/main.js 파일에서 addon 필드에 preset.js 파일을 추가한다.

```js
addons: [
    ...
    './preset.js'
  ],
```

이렇게 만든 탭에서 controls에서 설정한 args 값을 얻고 싶다면 useArgs 훅을 사용하면 된다.

```js
import { addons, types, useArgs } from '@storybook/manager-api'

const MyPanel = () => {
  const [args] = useArgs()
  return <pre>{args}</pre>
}
```

## 참고사이트

[Write an addon](https://storybook.js.org/docs/react/addons/writing-addons)
