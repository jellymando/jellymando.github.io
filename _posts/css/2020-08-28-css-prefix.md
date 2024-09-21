---
title: "[vendor prefix] css 접두어 webkit, moz, o, ms"
categories: [CSS]
tags: [css]
---

{:toc .large-only}

### css vendor prefix

- 표준 규약이 아닌 속성들은 브라우저에 따라 다른 방식으로 지원되기 때문에 속성 이름 앞에 접두사(prefix)를 붙여 크로스 브라우징해야 한다.

- 브라우저가 개선되면 필요 없는 접두어를 지워도 되지만, 낮은 버전의 브라우저를 사용하는 사용자를 위해 남겨둬야 할 때도 있다.

### 종류

- -webkit- : 구글, 사파리 브라우저
- -moz- : 모질라, 파이어폭스 브라우저
- -ms- : 인터넷 익스플로러 (대부분 생략)
- -o- : 오페라 브라우저

### 예시

```css
div {
  height: 200px;
  /* For Safari 5.1 to 6.0 */
  background: -webkit-linear-gradient(left, red, blue);
  /* For Opera 11.1 to 12.0 */
  background: -o-linear-gradient(right, red, blue);
  /* For Firefox 3.6 to 15 */
  background: -moz-linear-gradient(right, red, blue);
  /* Standard */
  background: linear-gradient(to right, red, blue);
}
```

### 참고사이트

[웹접근성 고려한 크로싱 브라우저 CSS 벤더 프리픽스 webkit,o,moz,ms 뜻](https://rgy0409.tistory.com/3018)<br/>
[[css] 브라우저 업체별 접두어(vendor prefix)](https://aboooks.tistory.com/271)<br/>
[스타일 시트 CSS 접두어 webkit, moz, ms, o 의미](https://mainia.tistory.com/3671)
