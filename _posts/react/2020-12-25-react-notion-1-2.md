---
title: "[React 스터디] 1 : 주요 개념 (2)"
categories: [React]
tags: [react]
---

{:toc .large-only}

## 여러 입력 처리

input 요소에서 여러 제어를 처리해야 하는 경우 각 요소에 name 속성을 추가하고 handler function의 event.target.name 값에 따라 수행 할 작업을 선택하도록 할 수 있습니다.

```js
class Reservation extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      isGoing: true,
      numberOfGuests: 2,
    };

    this.handleInputChange = this.handleInputChange.bind(this);
  }

  handleInputChange(event) {
    const target = event.target;
    const value = target.name === "isGoing" ? target.checked : target.value;
    const name = target.name;

    this.setState({
      [name]: value,
    });
  }

  render() {
    return (
      <form>
        <label>
          Is going:
          <input
            name="isGoing"
            type="checkbox"
            checked={this.state.isGoing}
            onChange={this.handleInputChange}
          />
        </label>
        <br />
        <label>
          Number of guests:
          <input
            name="numberOfGuests"
            type="number"
            value={this.state.numberOfGuests}
            onChange={this.handleInputChange}
          />
        </label>
      </form>
    );
  }
}
```

## 합성 vs 상속 특수화

React는 강력한 합성 모델을 가지고 있으며, 상속 대신 합성을 사용하여 컴포넌트 간에 코드를 재사용하는 것이 좋습니다.
어떤 컴포넌트들은 어떤 자식 엘리먼트가 들어올 지 미리 예상할 수 없는 경우가 있습니다. 범용적인 ‘박스’ 역할을 하는 Sidebar 혹은 Dialog와 같은 컴포넌트에서 특히 자주 볼 수 있습니다.
이러한 컴포넌트에서는 특수한 children prop을 사용하여 자식 엘리먼트를 출력에 그대로 전달하는 것이 좋습니다.

```js
function Dialog(props) {
  return (
    <FancyBorder color="blue">
      <h1 className="Dialog-title">{props.title}</h1>
      <p className="Dialog-message">{props.message}</p>
      {props.children}
    </FancyBorder>
  );
}

class SignUpDialog extends React.Component {
  constructor(props) {
    super(props);
    this.handleChange = this.handleChange.bind(this);
    this.handleSignUp = this.handleSignUp.bind(this);
    this.state = { login: "" };
  }

  render() {
    return (
      <Dialog
        title="Mars Exploration Program"
        message="How should we refer to you?"
      >
        <input value={this.state.login} onChange={this.handleChange} />
        <button onClick={this.handleSignUp}>Sign Me Up!</button>
      </Dialog>
    );
  }

  handleChange(e) {
    this.setState({ login: e.target.value });
  }

  handleSignUp() {
    alert(`Welcome aboard, ${this.state.login}!`);
  }
}
```

## React로 생각하기

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbF50kc%2FbtqGRQIFfRq%2FBt2JrV7MM8kkBfnsJx3mKk%2Fimg.png">

다섯개의 컴포넌트로 이루어진 앱을 한번 봅시다. 각각의 컴포넌트에 들어간 데이터는 이탤릭체로 표기했습니다.

- **FilterableProductTable(노란색)**: 예시 전체를 포괄합니다.
- **SearchBar(파란색)**: 모든 유저의 입력(user input) 을 받습니다.
- **ProductTable(연두색)**: 유저의 입력(user input)을 기반으로 데이터 콜렉션(data collection)을 필터링 해서 보여줍니다.
- **ProductCategoryRow(하늘색)**: 각 카테고리(category)의 헤더를 보여줍니다.
- **ProductRow(빨강색)**: 각각의 제품(product)에 해당하는 행을 보여줍니다.

이제 목업에서 컴포넌트를 확인하였으므로 이를 계층 구조로 나열해봅시다. 모형의 다른 컴포넌트 내부에 나타나는 컴포넌트는 계층 구조의 자식으로 나타냅니다.

- FilterableProductTable
  - SearchBar
  - ProductTable
    - ProductCategoryRow
    - ProductRow

데이터 모델을 렌더링하는 앱의 정적 버전을 만들기 위해 다른 컴포넌트를 재사용하는 컴포넌트를 만들고 props를 이용해 데이터를 전달해줍시다.
props는 부모가 자식에게 데이터를 넘겨줄 때 사용할 수 있는 방법입니다.
정적 버전을 만들기 위해 state를 사용하지 마세요. state는 오직 상호작용을 위해, 즉 시간이 지남에 따라 데이터가 바뀌는 것에 사용합니다.우리는 앱의 정적 버전을 만들고 있기 때문에 지금은 필요하지 않습니다.

[React 공식 문서 - 컴포넌트 State](https://ko.reactjs.org/docs/faq-state.html#what-is-the-difference-between-state-and-props)

앱을 만들 때 하향식(top-down)이나 상향식(bottom-up)으로 만들 수 있습니다. 다시 말해 계층 구조의 상층부에 있는 컴포넌트 (즉 FilterableProductTable부터 시작하는 것)부터 만들거나 하층부에 있는 컴포넌트 (ProductRow) 부터 만들 수도 있습니다. 간단한 예시에서는 보통 하향식으로 만드는 게 쉽지만 프로젝트가 커지면 상향식으로 만들고 테스트를 작성하면서 개발하기가 더 쉽습니다.

계층구조의 최상단 컴포넌트 (FilterableProductTable)는 prop으로 데이터 모델을 받습니다. 데이터 모델이 변경되면 ReactDOM.render()를 다시 호출해서 UI가 업데이트 됩니다.

애플리케이션은 다음과 같은 데이터를 가지고 있습니다.

- 제품의 원본 목록
- 유저가 입력한 검색어
- 체크박스의 값
- 필터링 된 제품들의 목록

각각 살펴보고 어떤 게 state가 되어야 하는 지 살펴봅시다. 이는 각 데이터에 대해 아래의 세 가지 질문을 통해 결정할 수 있습니다.

1. 부모로부터 props를 통해 전달됩니까? 그러면 확실히 state가 아닙니다.
2. 시간이 지나도 변하지 않나요? 그러면 확실히 state가 아닙니다.
3. 컴포넌트 안의 다른 state나 props를 가지고 계산 가능한가요? 그렇다면 state가 아닙니다.

결과적으로 애플리케이션은 다음과 같은 state를 가집니다.

- 유저가 입력한 검색어
- 체크박스의 값

애플리케이션이 가지는 각각의 state에 대해서

- state를 기반으로 렌더링하는 모든 컴포넌트를 찾으세요.
- 공통 소유 컴포넌트 (common owner component)를 찾으세요. (계층 구조 내에서 특정 state가 있어야 하는 모든 컴포넌트들의 상위에 있는 하나의 컴포넌트).
- 공통 혹은 더 상위에 있는 컴포넌트가 state를 가져야 합니다.
- state를 소유할 적절한 컴포넌트를 찾지 못하였다면, state를 소유하는 컴포넌트를 하나 만들어서 공통 오너 컴포넌트의 상위 계층에 추가하세요.

이 전략을 애플리케이션에 적용해봅시다.

- ProductTable은 state에 의존한 상품 리스트의 필터링해야 하고 SearchBar는 검색어와 체크박스의 상태를 표시해주어야 합니다.
- 공통 소유 컴포넌트는 FilterableProductTable입니다.
- 의미상으로도 FilterableProductTable이 검색어와 체크박스의 체크 여부를 가지는 것이 타당합니다.

좋습니다. state를 FilterableProductTable에 두기로 했습니다.
먼저 인스턴스 속성인 this.state = {filterText: '', inStockOnly: false} 를 FilterableProductTable의 constructor에 추가하여 애플리케이션의 초기 상태를 반영합니다.
그리고 나서 filterText와 inStockOnly를 ProductTable와 SearchBar에 prop으로 전달합니다.
마지막으로 이 props를 사용하여 ProductTable의 행을 정렬하고 SearchBar의 폼 필드 값을 설정하세요.
