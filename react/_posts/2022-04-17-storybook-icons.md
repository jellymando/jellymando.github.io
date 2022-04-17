---
layout: post
title: "[Storybook] 페이지에 Icons 컴포넌트 나열하기"
sitemap: false
---

{:toc .large-only}

아이콘들을 export하고 storybook에서 맵핑하는 부분이 헷갈려서 정리해둔다.

## 아이콘 컴포넌트 추가

우선 아이콘 svg를 jsx나 tsx 형태로 바꿔서 파일을 추가해준다.

## 아이콘들을 export 하는 파일 추가

Icons.ts 파일을 생성한다. (이름은 상관없다)

위에서 만들어준 아이콘 컴포넌트들을 여기서 export 해준다.

```js
export { default as Bell } from "./Bell";
export { default as User } from "./User";
```

## storybook에서 불러올 default Icons 컴포넌트 추가

```js
import React from "react";
import * as Icons from "./Icons";

type IconType = keyof typeof Icons;
export const IconTypes = Object.keys(Icons) as IconType[];

export default function Icon({
  name,
  width,
  height,
  color
}: {
  name: IconType;
  width?: number;
  height?: number;
  color?: string;
}) {
  const Icon = Icons[name];
  return <Icon width={width} height={height} color={color} />;
}
```

Icons 폴더에 index 파일을 생성하고 Icons.ts를 import 해준다.

`keyof typeof`를 통해 IconType을 정의하고, IconTypes 변수에 Icons 객체를 배열로 변환하여 export 한다.

Icons 배열의 각 컴포넌트에 props를 담아 return 한다.

## storybook에서 Icons 페이지 생성

```js
import Icons, { IconTypes } from "@/components/Icons";

export default {
  title: "Icons",
  component: Icons
} as ComponentMeta<typeof Icons>;

const Template: ComponentStory<typeof Icons> = (args) => (
  <>
    {IconTypes.map((icon) => (
      <Icons name={icon} {...args} />
    ))}
  </>
);
```

이제 storybook에서 IconTypes를 map으로 순회하여 아이콘 컴포넌트들을 페이지에 생성할 수 있다.

## 참고사이트

[Storybook을 활용하여 본격적으로 디자인 시스템 구축하기](https://velog.io/@velopert/create-your-own-design-system-with-storybook#4-3-icon-%EB%A7%8C%EB%93%A4%EA%B8%B0)
