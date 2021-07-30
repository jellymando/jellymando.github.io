---
layout: post
title: "autocomplete : 자동완성 허용 설정"
sitemap: false
---

{:toc .large-only}

```html
<input type="number" name="cc-number" id="cc-number" autocomplete="off" />
```

- 사용자에게 어떤 정보에 대한 자동완성을 원하는지 안내할 수 있다.
- `<input>`, `<textarea>`, `<select>`, `<form>` 요소가 다음 조건을 만족해야 사용할 수 있다.
  - name 또는 id 특성 존재
  - <form> 요소의 자손일 것
  - 양식에 제출 (en-US) 버튼이 있을 것
- `off`로 설정하면 브라우저가 이 필드에 값을 자동으로 넣는 것을 금지한다. 보안상 문제로 자동완성을 사용하지 않아야 할 경우 지정
  - 대부분의 최신 브라우저에서는 `autocomplete`을 off로 지정하더라도 브라우저가 사용자에게 계정 이름과 비밀번호 저장 여부를 묻는 것을 막을 수 없으며, 저장한 값을 사용해 자동완성하는 것도 막을 수 없다.

<br/>

[HTML autocomplete 특성](https://developer.mozilla.org/ko/docs/Web/HTML/Attributes/autocomplete)
