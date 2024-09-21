---
title: "async와 defer 의미, 실행 순서, 공통점, 차이점"
categories: [Javascript]
tags: [javascript, async, defer]
---

{:toc .large-only}

### script

기본적으로 웹 브라우저가 외부 자바스크립트를 불러오는 일반 script 태그를 만나게 되면, 우선 해당 스크립트를 내려받아 해석하고 실행(execute)할 때까지 웹 문서의 HTML 코드 parsing 작업을 잠시 뒤로 미룬다.

async 혹은 defer 된 스크립트는 문서 parsing 작업의 중단 없이 동시에 내려받게 되며, 선택적으로 onload handler를 지정해서 일반적인 초기화 작업도 진행할 수 있다.

### script async

async 속성을 쓰면 문서를 파싱하는 동안 스크립트를 만나면 문서 파싱과 함께 스크립트를 다운받고 스크립트 다운이 완료되면 즉시 스크립트를 실행하게 된다.

다운로드가 끝나고 스크립트를 실행하는 동안은 문서(HTML) 파싱을 멈추고 스크립트 실행이 끝난 후 남은 문서를 읽는다.

모든 스크립트에 async 속성이 있다면 모듈 스크립트와 모든 의존 스크립트 지연 큐에서 실행돼 함께 병렬로 불러오며 이와 동시에 스크립트를 다운받고 실행시킨다.

문서(HTML)에서 아직 id나 class를 읽지도 않았는데 스크립트가 DOM을 참조하고 있으면 오류가 생기므로 DOM을 조작하지 않는 코드에만 쓰자.

```html
<script async src="myAsyncScript.js" onload="myInit()"></script>
```

### script defer

브라우저가 defer 스크립트를 만났을 때 스크립트를 다운로드하지만 문서 파싱을 멈추지 않고 끝까지 수행하고 스크립트는 `</html>` 태그를 만났을 때 실행한다.

즉 DOMContentLoaded 발생 이전에 실행해야 함을 나타내는 불리언 속성이다.

일반 스크립트를 `<body>` 태그의 맨 마지막 줄에 위치시켜 작성하는 것과 비슷한 효과를 준다.

DOM을 조작해 HTML 의존성이 있을 때 문서(HTML)을 모두 파싱한 후 실행되어야 할 때 쓰도록 하자.

### 정리

| 구분   |                              async                              |                                 defer |
| ------ | :-------------------------------------------------------------: | ------------------------------------: |
| 공통점 | 스크립트를 다운로드하는 동안 문서(HTML) 파싱이 중단되지 않는다. |
| 차이점 |             스크립트를 다운로드됐을 때 곧바로 실행              | 문서(HTML)을 완전히 다 읽은 후에 실행 |

<br/>

<img src="https://appletree.or.kr/blog/images/javascript_execution.jpg">

<br/>

[](https://webroadcast.tistory.com/15)

[script 태그의 async와 defer 속성](https://appletree.or.kr/blog/web-development/javascript/script-%ED%83%9C%EA%B7%B8%EC%9D%98-async%EC%99%80-defer-%EC%86%8D%EC%84%B1/)
