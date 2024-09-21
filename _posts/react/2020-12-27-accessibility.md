---
title: "[React 스터디] 2 : 접근성"
categories: [REACT]
tags: [react]
---

{:toc .large-only}

## 접근성이란?

사용자가 신체적 불편함이나 장애 여부와 상관없이 웹에 접근할 수 있도록 고려하는 것으로 img태그에 대한 대체 텍스트, 건너뛰기 링크, 레이블 제공 등으로 접근성을 높일 수 있다.

## 시맨틱 HTML

```js
class Table extends React.Component {
  render() {
    return (
      <table>
        <tr>
          <Columns />
        </tr>
      </table>
    );
  }
}

class Columns extends React.Component {
  render() {
    return (
      <div>
        <td>Hello</td>
        <td>World</td>
      </div>
    );
  }
}
```

`<Table />`의 출력 결과는 다음과 같습니다.

```js
<table>
  <tr>
    <div>
      <td>Hello</td>
      <td>World</td>
    </div>
  </tr>
</table>
```

렌더링 된 HTML이 유효하려면 `<Columns />`가 여러 `<td>` 엘리먼트만 반환해야 합니다. `<Columns />`의 render() 안에 부모 div로 자식들을 감싼다면 렌더링 된 HTML은 유효하지 않습니다. Fragments는 이 문제를 해결해줍니다.

```js
class Columns extends React.Component {
  render() {
    return (
      <React.Fragment>
        <td>Hello</td>
        <td>World</td>
      </React.Fragment>
    );
  }
}
```

올바른 `<Table />`의 출력 결과는 아래와 같습니다.

```js
<table>
  <tr>
    <td>Hello</td>
    <td>World</td>
  </tr>
</table>
```

배열의 각 항목을 매핑할 때에도 사용할 수 있습니다.

```js
function Glossary(props) {
  return (
    <dl>
      {props.items.map((item) => (
        // 항목을 매핑할 때 Fragment는 반드시 `key` 프로퍼티가 있어야 합니다.
        <Fragment key={item.id}>
          <dt>{item.term}</dt>
          <dd>{item.description}</dd>
        </Fragment>
      ))}
    </dl>
  );
}
```

> 단축 문법 : 만약, Fragment 태그에 어떤 props도 필요하지 않고, 사용하고 있는 도구에서 지원한다면, 아래와 같이 짧게 줄여 쓸 수 있습니다.

```js
<>
  <dt>{item.term}</dt>
  <dd>{item.description}</dd>
</>
```

## 포커스 컨트롤

React에서 포커스를 지정하려면, DOM 엘리먼트에 ref를 사용할 수 있습니다.
이를 사용해 JSX 컴포넌트 클래스 안에서 엘리먼트에 대한 ref를 먼저 생성합니다.

가끔씩 부모 컴포넌트가 자식 컴포넌트 내의 엘리먼트에 포커스를 잡아야 할 때가 있습니다. 이때는 자식 컴포넌트에 특별한 프로퍼티를 주어 DOM ref를 부모 컴포넌트로 노출하는 방식으로 부모의 ref를 자식의 DOM 노드에 넘겨줄 수 있습니다.

```js
function CustomTextInput(props) {
  return (
    <div>
      <input ref={props.inputRef} />
    </div>
  );
}

class Parent extends React.Component {
  constructor(props) {
    super(props);
    this.inputElement = React.createRef();
  }
  render() {
    return <CustomTextInput inputRef={this.inputElement} />;
  }
}

// 이제 필요할 때마다 포커스를 잡을 수 있습니다.
this.inputElement.current.focus();
```

## 마우스와 포인터 이벤트

아래는 클릭 이벤트로 인해 접근성이 떨어지게 되는 예시입니다. 열린 팝오버의 바깥을 클릭해 팝오버를 닫을 수 있는 ‘외부 클릭 패턴(outside click pattern)’입니다.

onBlur와 onFocus 같은 적절한 이벤트 핸들러를 사용하여 같은 기능을 제공할 수 있습니다.

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbWoLkx%2FbtqG6I4N2e1%2FoWBzC09D1Th1ccKCTSWHKK%2Fimg.gif">

```js
class BlurExample extends React.Component {
  constructor(props) {
    super(props);

    this.state = { isOpen: false };
    this.timeOutId = null;

    this.onClickHandler = this.onClickHandler.bind(this);
    this.onBlurHandler = this.onBlurHandler.bind(this);
    this.onFocusHandler = this.onFocusHandler.bind(this);
  }

  onClickHandler() {
    this.setState((currentState) => ({
      isOpen: !currentState.isOpen,
    }));
  }

  // setTimeout을 사용해 다음 순간에 팝오버를 닫습니다.
  // 엘리먼트의 다른 자식에 포커스가 맞춰져있는지 확인하기 위해 필요합니다.
  // 새로운 포커스 이벤트가 발생하기 전에
  // 블러(blur) 이벤트가 발생해야 하기 때문입니다.
  onBlurHandler() {
    this.timeOutId = setTimeout(() => {
      this.setState({
        isOpen: false,
      });
    });
  }

  // 만약 자식이 포커스를 받으면, 팝오버를 닫지 않습니다.
  onFocusHandler() {
    clearTimeout(this.timeOutId);
  }

  render() {
    // React는 블러와 포커스 이벤트를 부모에 버블링해줍니다.
    return (
      <div onBlur={this.onBlurHandler} onFocus={this.onFocusHandler}>
        <button
          onClick={this.onClickHandler}
          aria-haspopup="true"
          aria-expanded={this.state.isOpen}
        >
          Select an option
        </button>
        {this.state.isOpen && (
          <ul>
            <li>Option 1</li>
            <li>Option 2</li>
            <li>Option 3</li>
          </ul>
        )}
      </div>
    );
  }
}
```

## 개발 및 테스트 도구

#### 키보드

1. 마우스의 연결을 해제하세요.
2. Tab과 Shift+Tab을 사용해 이동하세요.
3. Enter를 사용해 엘리먼트를 활성화하세요.
4. 메뉴와 드롭다운과 같은 일부 엘리먼트는 필요하다면 키보드 방향키를 사용해 조작합니다.

#### eslint-plugin-jsx-a11y

ESLint 플러그인인 eslint-plugin-jsx-a11y는 JSX 내의 접근성 문제에 대해 즉각적인 AST 린팅 피드백을 제공합니다. 많은 IDE가 코드 분석과 소스 코드 창에 이런 결과를 통합할 수 있도록 해줍니다.

Create React App에서는 해당 플러그인의 일부 규칙들이 활성화되어 있습니다. 더 많은 접근성 기능을 활성화하려면, 프로젝트 최상위에 아래와 같이 .eslintrc 파일을 생성합니다.

```js
{
  "extends": ["react-app", "plugin:jsx-a11y/recommended"],
  "plugins": ["jsx-a11y"]
}
```

<br/>
[React 공식 문서 - 접근성](https://ko.reactjs.org/docs/accessibility.html)
