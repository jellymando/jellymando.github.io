---
title: "동등 연산자 == 와 일치 연산자 === 의 차이🤨"
categories: [JAVASCRIPT]
tags: [javascript]
---

{:toc .large-only}

## == (동등 연산자 : Equality operator)

- 피연산자가 서로 다른 타입이면 타입을 강제로 변환하여 비교한다.
- 변환한 내용이 같은 경우 참(true)을 반환한다.

## === (일치 연산자 : Identity operator)

- 피연산자의 자료형까지 일치하는지 비교한다.
- 변환하지 않아도 내용이 같은 경우 참(true)을 반환한다.

<br/>

| x | y | == | === |
| undefined | undefined | true | true |
| null | null | true | true |
| true | true | true | true |
| 'foo' | 'foo' | true | true |
| +0 | -0 | true | true |
| 0 | false | true | <span style="color:red;">false</span> |
| "" | false | true | <span style="color:red;">false</span> |
| "" | 0 | true | <span style="color:red;">false</span> |
| '0' | 0 | true | <span style="color:red;">false</span> |
| [1, 2] | '1, 2' | true | <span style="color:red;">false</span> |
| 'foo' | new String('foo') | true | <span style="color:red;">false</span> |
| undefined | null | true | <span style="color:red;">false</span> |
| false | undefined | <span style="color:red;">false</span> | <span style="color:red;">false</span> |
| false | null | <span style="color:red;">false</span> | <span style="color:red;">false</span> |
