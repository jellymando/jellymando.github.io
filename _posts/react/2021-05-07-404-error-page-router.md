---
title: "리액트를 다루는 기술 : 리액트 라우터로 SPA 개발하기"
categories: [REACT]
tags: [react, react router]
---

{:toc .large-only}

### Route 컴포넌트로 특정 주소에 컴포넌트 연결

Route라는 컴포넌트를 사용하면 어떤 규칠을 가진 경로에 어떤 컴포넌트를 보여줄 지 정의할 수 있습니다.

/ 경로를 사용하는 Route에 exact라는 props를 설정하지 않으면 /about 경로가 / 규칙에도 일치하기 때문에 두 컴포넌트가 모두 나타나게 됩니다.

```js
<Route path="/" component={Home} exact/>
<Route path="/about" component={About}/>
```

### Link 컴포넌트를 사용하여 다른 주소로 이동하기

Link 컴포넌트는 클릭하면 다른 주소로 이동시켜 주는 컴포넌트입니다.

일반 웹 애프리케이션에서는 a 태그를 사용하여 페이지를 전환하지만, 리액트 라우터를 사용할 때는 a 태그를 사용하여 페이지를 전환하면 컴포넌트들이 리렌더링 되기 때문에 Link 컴포넌트를 사용해야 합니다.

```js
<Link to="/">홈</Link>
<Link to="/about">소개</Link>
```

### Route 하나에 여러 개의 path 설정하기

path props를 배열로 설정해 주면 여러 경로에서 같은 컴포넌트를 보여줄 수 있습니다.

```js
<Route path={['/about', '/info']} component={About}>
```

### Switch

Switch 컴포넌트는 여러 Route를 감싸서 그중 일치하는 단 하나의 라우트만을 렌더링시켜 줍니다.

Switch를 사용하면 모든 규칙과 일치하지 않을 때 보여 줄 Not Found 페이지도 구현할 수 있습니다.

```js
<Switch>
  <Route path="/" component={Home} exact />
  <Route path={["/about", "/info"]} component={About} />
  <Route path="/profiles" component={Profiles} />
  <Route
    // path를 따로 정의하지 않으면 모든 상황에 렌더링됨
    render={({ location }) => (
      <div>
        <h2>이 페이지는 존재하지 않습니다.</h2>
        <p>{location.pathname}</p>
      </div>
    )}
  />
</Switch>
```
