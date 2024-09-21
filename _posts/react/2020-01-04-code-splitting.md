---
title: "[React 스터디] 3 : 코드 분할"
categories: [React]
tags: [react]
---

{:toc .large-only}

## 번들링

대부분 React 앱들은 Webpack, Rollup 또는 Browserify 같은 툴을 사용하여 여러 파일을 하나로 병합한 “번들된” 파일을 웹 페이지에 포함하여 한 번에 전체 앱을 로드할 수 있습니다.

번들이 거대해지는 것을 방지하기 위한 좋은 해결방법은 번들을 “나누는” 것입니다.

앱에 코드 분할을 도입하는 가장 좋은 방법은 동적 import() 문법을 사용하는 방법입니다.

#### before

```js
// app.js
import { add } from "./math";

console.log(add(16, 26));

// math.js
export function add(a, b) {
  return a + b;
}
```

#### after

```js
import("./math").then((math) => {
  console.log(math.add(16, 26));
});
```

## Suspense

Suspense를 사용하면 컴포넌트가 렌더링되기 전까지 기다릴 수 있습니다.

```js
// 이것은 프라미스가 아닙니다. Suspense 통합에서 만들어낸 특별한 객체입니다.
const resource = fetchProfileData();

function ProfilePage() {
  return (
    <Suspense fallback={<h1>Loading profile...</h1>}>
      <ProfileDetails />
      <Suspense fallback={<h1>Loading posts...</h1>}>
        <ProfileTimeline />
      </Suspense>
    </Suspense>
  );
}

function ProfileDetails() {
  // 아직 로딩이 완료되지 않았더라도, 사용자 정보 읽기를 시도합니다
  const user = resource.user.read();
  return <h1>{user.name}</h1>;
}

function ProfileTimeline() {
  // 아직 로딩이 완료되지 않았더라도, 게시글 읽기를 시도합니다
  const posts = resource.posts.read();
  return (
    <ul>
      {posts.map((post) => (
        <li key={post.id}>{post.text}</li>
      ))}
    </ul>
  );
}
```

<br/>
화면 상에 `<ProfilePage>`를 렌더링할 때에 아래와 같은 일들이 벌어집니다.

1. fetchProfileData() 요청을 발동시킵니다.
2. `<ProfilePage>`의 렌더링을 시도합니다.
3. `<ProfileDetails>`의 렌더링을 시도합니다. resource.user.read()를 호출합니다. 아직 불러온 데이터가 아무 것도 없으므로 다른 컴포넌트의 렌더링을 시도합니다.
4. `<ProfileTimeline>`의 렌더링을 시도합니다. resource.posts.read()를 호출합니다. 또 한번, 아직 데이터가 없으므로 다른 컴포넌트의 렌더링을 시도합니다.
5. 렌더링을 시도할 컴포넌트가 남아있지 않습니다. `<ProfileDetails>`가 정지된 상태이므로, React는 트리 상에서 `<ProfielDetails>` 위에 존재하는 것 중 가장 가까운 `<Suspense>` Fallback을 찾습니다. 그것은 `<h1>`Loading profile...`</h1>`입니다. 일단, 지금으로서는 할 일이 다 끝났습니다.

## React.lazy

React.lazy 함수를 사용하면 동적 import를 사용해서 컴포넌트를 렌더링 할 수 있습니다.

```js
import React, { Suspense } from "react";

const OtherComponent = React.lazy(() => import("./OtherComponent"));
const AnotherComponent = React.lazy(() => import("./AnotherComponent"));

function MyComponent() {
  return (
    <div>
      <Suspense fallback={<div>Loading...</div>}>
        <section>
          <OtherComponent />
          <AnotherComponent />
        </section>
      </Suspense>
    </div>
  );
}
```

<br/>
lazy 컴포넌트는 Suspense 컴포넌트 하위에서 렌더링되어야 하며, 하나의 Suspense 컴포넌트로 여러 lazy 컴포넌트를 감쌀 수도 있습니다.

## 비동기식 반응 라우터

특정 Route에 있을 때만 컴포넌트를 로드할 수 있습니다.

다른 컴포넌트와 함께 사용할 때 특정 Route에 있을 때만 로드되도록 컴포넌트를 포장할 수 있습니다.

```js
import React, { Suspense, lazy } from "react";
import { BrowserRouter as Router, Route, Switch } from "react-router-dom";

const FunComponent = lazy(() => import("./FunComponent"));
const TerribleComponent = lazy(() => import("./TerribleComponent"));
const TestComponent = lazy(() => import("./TestComponent"));
const LoadingMessage = () => "I'm loading...";

const App = () => (
  <Suspense fallback={<LoadingMessage />}>
    <Switch>
      <Route path="/fun">
        <FunComponent />
      </Route>

      <Route path="/terrible">
        <TerribleComponent />
      </Route>

      <Route>
        <TestComponent />
      </Route>
    </Switch>
  </Suspense>
);
```

<br/>
[Webpack - 모듈시스템과 번들링의 이해](https://velog.io/@bigbrothershin/Webpack-JS-ES6-%EB%AA%A8%EB%93%88%EC%8B%9C%EC%8A%A4%ED%85%9C-%EC%9D%B4%ED%95%B4)<br/>
[React 공식 문서 - 코드 분할](https://ko.reactjs.org/docs/code-splitting.html)<br/>
[React 공식 문서 - 데이터를 가져오기 위한 Suspense (실험 단계)](https://ko.reactjs.org/docs/concurrent-mode-suspense.html)<br/>
[Async React using React Router & Suspense](https://itnext.io/async-react-using-react-router-suspense-a86ade1176dc)
