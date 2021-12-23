---
layout: post
title: '[VSCode] React Snippets 비교'
sitemap: false
---

{:toc .large-only}

## React Snippets

새 컴퓨터에 VSCode를 설치하고, 이것저것 환경 세팅을 하면서 리액트 스니펫을 설치하게 되었다.

<img src="/assets/img/blog/2021-12-23-react-snippets.png" style="margin-bottom:20px">

마켓플레이스에서 react만 검색해도 많은 Snippets들이 나온다.

처음에는 가장 상단의, 다운로드수가 가장 많은 ES7 React/Redux/GraphQL/React-Native snippets을 설치했었다.

하지만 사용하다보니 기존에 쓰던 스니펫과 다름을 느꼈고, GraphQL, React-Native는 사용하지 않기 때문에 다른 확장을 설치하기로 했다.

## ES7 React/Redux/GraphQL/React-Native snippets

| 단축어 | 반환값                                             |
| ------ | -------------------------------------------------- |
| imr    | import React from 'react'                          |
| imrse  | import React, { useState, useEffect } from 'react' |
| rcc    | Class Component                                    |
| rfcp   | Function Component                                 |
| redux  | import { connect } from 'react-redux'              |

#### rcredux

```js
import React, { Component } from 'react'
import { connect } from 'react-redux'

export class FileName extends Component {
  render() {
    return <div>$4</div>
  }
}

const mapStateToProps = (state) => ({})

const mapDispatchToProps = {}

export default connect(mapStateToProps, mapDispatchToProps)(FileName)
```

단축어 종류가 굉장히 많다.

하지만 함수형 컴포넌트 단축어가 `rfcp` 인게 맘에 들지 않아서.. (단순한 개인취향)

## Simple React Snippets

다음으로 다운로드 수가 많았던 스니펫이다.

| 단축어 | 반환값                                             |
| ------ | -------------------------------------------------- |
| imr    | import React from 'react'                          |
| imrse  | import React, { useState, useEffect } from 'react' |
| cc     | Class Component                                    |
| fc     | Function Component                                 |

`imr`, `imrse` 단축어는 ES7 React/Redux/GraphQL/React-Native snippets과 동일하다.

클래스형/함수형 컴포넌트 단축어는 Simple React Snippets가 좀 더 간결하다.

하지만 Redux를 제공하지 않아서 패스.

## React/Redux/react-router Snippets

| 단축어    | 반환값                                |
| --------- | ------------------------------------- |
| imr       | import React from 'react'             |
| rcc       | Class Component                       |
| rsc       | Function Component                    |
| imconnect | import { connect } from 'react-redux' |

#### container

```js
import { connect } from 'react-redux'
import component from '../components/component'
import { actionCreator } from '../actionPath'

const mapStateToProps = (state, ownProps) => ({})

const mapDispatchToProps = {}

export default connect(mapStateToProps, mapDispatchToProps)(component)
```

전체적으로 ES7 React/Redux/GraphQL/React-Native snippets와 단축어가 다르다.

`imrse`는 없고, redux 부분도 처음 스니펫은 `redux`, `rcredux`인 것에 반해 React/Redux/react-router Snippets은 `imconnect`, `container`와 같이 redux라는 단어가 생략되어 있다.

앞으로 주로 React, Redux만 사용할 것 같기 때문에 불필요한 단축어가 없는 후자를 선택했다.

그리고 클래스형/함수형 컴포넌트의 단축어 `rcc`, `rsc`가 그동안 써왔던 단축어이기 때문에 고른 이유가 가장 크다.

## 참고사이트

[ES7 React/Redux/GraphQL/React-Native snippets](https://github.com/dsznajder/vscode-es7-javascript-react-snippets)<br/>
[React/Redux/react-router Snippets](https://github.com/discountry/vscode-react-redux-react-router-snippets)
