---
title: "useEffect 의존성 배열 없애는 방법"
categories: [REACT]
tags: [react, useEffect]
---

{:toc .large-only}

## 의존성 배열을 사용하는 경우

- 상태값을 이용해 api를 호출할 때

```js
useEffect(() => {
  fetchUser(userId).then((data) => setUser(data));
}, [userId]);
```

## 의존성 배열을 잘못 관리하면 생기는 일

의존성 배열에 입력해야 할 값을 입력하지 않으면 오래된 값을 참조하는 문제가 발생한다.

```js
function MyComponent() {
  const [value1, setValue1] = useState(0);
  const [value2, setValue2] = useState(0);
  useEffect(() => {
    const id = setTimeout(() => console.log(value1, value2), 1000);
    return () => clearInterval(id);
  }, [value1]);
  return (
    <div>
      <button onClick={() => setValue1(value1 + 1)}>value1 증가</button>
      <button onClick={() => setValue2(value2 + 1)}>value2 증가</button>
    </div>
  );
}
```

위 코드에서 useEffect의 의존성 배열에 value2를 넣지 않았다.

때문에 value2가 변경되어도 부수 효과 함수 안의 value2 값은 갱신되지 않는다.

## eslint 규칙

리액트에서 제공하는 exhaustive-deps eslint 규칙을 사용하면 잘못 사용한 의존성 배열을 찾아서 알려준다.

의존성 배열에서 실수를 하는 경우가 많고, 의존성 배열 때문에 발생한 버그는 원인 파악도 힘들기 때문에 플러그인을 사용하는 것이 좋다.

## 의존성 배열을 없애는 방법

- 부수 효과 함수 내에서 분기 처리하기

```js
function Profile({ userId }) {
  const [user, setUser] = useState();
  async function fetchAndSetUser(needDetail) {
    const data = await fetchUser(userId, needDetail);
    setUser(data);
  }
  useEffect(() => {
    if (!user || user.id !== userId) {
      fetchAndSetUser(false);
    }
  });
}
```

의존성 배열을 입력하지 않고 if 문으로 `fetchAndSetUser` 호출 시점을 관리한다.

이렇게 하면 렌더링될 때마다 user 값을 체크하여 useEffect에서 갱신된 값을 가져온다.

하지만 렌더링될 때마다 부수 효과 함수가 실행되기 때문에 최적화에는 비효율적인 것 같다.

- useState의 set 함수에 콜백 함수 전달하기

```js
function MyComponent() {
  const [count, setCount] = useState(0);
  useEffect(() => {
    function onClick() {
      setCount((prev) => prev + 1);
    }
    window.addEventListener("click", onClick);
    return () => window.removeEventListener("click", onClick);
  });
}
```

set 함수에 콜백 함수를 전달하면 이전 상태값을 매개변수로 받는다.

의존성 배열에서 count를 제거해도 값이 갱신된다.

- useReducer 활용하기

많은 상태값을 참조해야 할 때는 useReducer 훅을 사용하는 것이 좋다.

#### 의존성 배열 사용

```js
function Timer({ initialTotalSeconds }) {
  const [hour, setHour] = useState(Math.floor(initialTotalSeconds / 3600));
  const [minute, setMinute] = useState(
    Math.floor((initialTotalSeconds % 3600) / 60)
  );
  const [second, setSecond] = useState(initialTotalSeconds % 60);
  useEffect(() => {
    const id = setInteval(() => {
      if (second) {
        setSecond(second - 1);
      } else if (minute) {
        setMinute(minute - 1);
        setSecond(59);
      } else if (hour) {
        setHour(hour - 1);
        setMinute(59);
        setSecond(59);
      }
    }, 1000);
    return () => clearInterval(id);
  }, [hour, minute, second]);
}
```

#### useReducer 사용

```js
function Timer({ initialTotalSeconds }) {
  const [state, dispatch] = useReducer(reducer, {
    hour: Math.floor(initialTotalSeconds / 3600),
    minute: Math.floor((initialTotalSeconds % 3600) / 60),
    second: initialTotalSeconds % 60,
  });
  const { hour, minute, second } = state;
  useEffect(() => {
    const id = setInterval(dispatch, 1000);
    return () => clearInterval(id);
  });
}
function reducer(state) {
  const { hour, minute, second } = state;
  if (second) {
    return { ...state, second: second - 1 };
  } else if (minute) {
    return { ...state, minute: minute - 1, second: 59 };
  } else if (hour) {
    return { ...state, hour: hour - 1, minute: 59, second: 59 };
  } else {
    return state;
  }
}
```

`hour, minute, second` 상태값을 모두 useReducer 훅으로 관리한다.

useReducer 훅의 두 번째 매개변수는 초기 상태값이며 상태값을 변경하는 로직은 reducer 함수에서 구현한다.

useReducer 훅을 사용하면 다양한 상태값과 액션을 관리하기 쉽고 재사용성이 높다.

- useRef 활용하기

```js
function MyComponent({ onClick }) {
  const onClickRef = useRef();
  useEffect(() => {
    onClickRef.current = onClick;
    window.addEventListner("click", () => {
      onClickRef.current();
    });
  });
}
```

onClick을 useRef에 저장한다. (렌더링 결과와 무관한 값을 저장해야 한다.)

useRef에 저장된 값이 변경되어도 컴포넌트가 다시 렌더링되지 않기 때문에 의존성 배열을 제거할 수 있다.

useEffect에서 useRef 값을 지정하는 이유는 컴포넌트의 렌더링 결과가 돔에 반영된 이후에 값을 지정하기 위해서다.

## 참고사이트

실전 리액트 프로그래밍 4.2장<br/>
[ESLint 플러그인](https://ko.reactjs.org/docs/hooks-rules.html#eslint-plugin)
