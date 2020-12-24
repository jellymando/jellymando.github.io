---
layout: post
title: "1 : 타입스크립트란? & 기본 설치"
sitemap: false
---

{:toc .large-only}

## 타입스크립트란?

- Microsoft가 개발한 프로그래밍 언어
- 정적 타입 시스템(static type system)을 도입한 자바스크립트
- 자바스크립트로 컴파일되는, 자바스크립트 타입이 있는 상위집합(superset)
- .ts 확장자를 .js로 컴파일하여 사용
- 타입 검사기를 통해 프로그램 실행 전에 확인 - 런타임이 아닌 컴파일 환경에서 에러를 잡을 수 있음

> [슈퍼셋이란?](zetawiki.com/wiki/%EB%B6%80%EB%B6%84%EC%A7%91%ED%95%A9,_%EC%A7%84%EB%B6%80%EB%B6%84%EC%A7%91%ED%95%A9,_%EC%83%81%EC%9C%84%EC%A7%91%ED%95%A9,_%EC%A7%84%EC%83%81%EC%9C%84%EC%A7%91%ED%95%A9,_%ED%8F%AC%ED%95%A8%EA%B4%80%EA%B3%84)

### 타입스크립트 설치

VSCode는 타입스크립트 지원 기능이 내장되어 있어 별도의 설정 없이도 .ts, tsconfig.json 등의 타입스크립트 파일을 인식할 수 있다. 단, 컴파일러는 설치되어 있지 않기 때문에 별도로 설치해야 한다.

```js
yarn add --dev typescript
```

tsconfig.json 파일을 생성하기 위해 아래 명령어를 입력한다.

```js
yarn run tsc --init
```

tsconfig.json 의 compilerOptions를 설정한다.

```js
{
  "compilerOptions": {
    "sourceMap": true,  // 소스맵(*.map) 파일 생성 여부
    "jsx": "react"  // Resolve: Cannot use JSX unless '--jsx' flag is provided
  }
}
```

.js 파일 확장자를 .ts / .tsx 로 변경한다.

#### 예제

```js
//index.tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import App from "./App";

ReactDOM.render(
  <React.StrictMode>
    <App firstName="hyuna" lastName="lee" />
  </React.StrictMode>,
  document.getElementById("root")
);
```

```js
//App.tsx
import * as React from "react";

interface Props {
  firstName: string;
  lastName: string;
}

class App extends React.Component<Props> {
  render() {
    const { firstName, lastName } = this.props;

    return (
      <div>
        {firstName} {lastName}
      </div>
    );
  }
}

export default App;
```

```js
//tsconfig.json
{
  "compilerOptions": {
    "target": "es5",
    "module": "esnext",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true,
    "lib": ["dom", "dom.iterable", "esnext"],
    "allowJs": true,
    "allowSyntheticDefaultImports": true,
    "moduleResolution": "node",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "noEmit": true,
    "jsx": "react"
  },
  "include": ["src"]
}
```
