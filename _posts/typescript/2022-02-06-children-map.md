---
title: "React에서 children을 map 돌리기"
categories: [Typescript]
tags: [typescript]
---

{:toc .large-only}

## 목적

컴포넌트에 `ul`과 `li` 구조를 만들고, children을 전달받아 map을 돌려 `li`를 리턴하려고 한다.

## 문제

```js
export default function Form(children: JSX.Element[]) {
  return (
    <form>
      <ul>
        {children.map((el, i) => (
          <li key={i}>{el}</li>
        ))}
      </ul>
    </form>
  );
}
```

```js
<Form>
  <Input />
  <Input />
  <Input />
  <Input />
</Form>
```

이렇게 짜니, `Form` 컴포넌트를 호출한 곳에서 `'{ children: Element[]; }' 형식에 'Element[]' 형식의 length, pop, push, concat 외 29개 속성이 없습니다.` 라는 ts 에러가 뜬다.

`children`이 `props` 객체 내부의 값이기 때문에 생긴 에러였다.

<img src="/assets/img/blog/2022-02-06-children-map_01.png">

## 해결

`React.Children`을 통해 `children`에 접근할 수 있다.

```js
const Form = (props: { children: JSX.Element[] }) => {
  return (
    <form>
      <ul>
        {React.Children.map(props.children, (el, i) => (
          <li key={i}>{el}</li>
        ))}
      </ul>
    </form>
  );
};
```

아래와 같이 간략하게 고칠 수 있다.

```js
const Form = ({ children }: { children: JSX.Element[] }) => {
  return (
    <form>
      <ul>
        {children.map((el, i) => (
          <li key={i}>{el}</li>
        ))}
      </ul>
    </form>
  );
};
```

## 참고사이트

[How to iterate through a Component's Children in Typescript React?](https://stackoverflow.com/questions/34030328/how-to-iterate-through-a-components-children-in-typescript-react)<br/>
[React 컴포넌트의 props(인자)](https://velog.io/@alajillo/React.Children#react-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8%EC%9D%98-props%EC%9D%B8%EC%9E%90)<br/>
[React.Children](https://ko.reactjs.org/docs/react-api.html#reactchildren)
