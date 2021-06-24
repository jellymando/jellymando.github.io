---
layout: post
title: "[IE] 체크박스 디자인 커스텀하기 + 체크박스 클릭 시 맨 위로 이동하는 문제"
sitemap: false
---

{:toc .large-only}

### IE 9 버전 밑으로는 :before, :after 를 지원하지 않는다.

때문에 일반적인 `:before` 나 `:after` 를 사용하는 체크박스 커스텀은 하지 못하고, 직접 html 엘리먼트를 추가해서 체크박스를 디자인해줘야 한다.

#### html

```html
<div class="checkbox-wrap">
  <input id="checkbox" type="checkbox" />
  <label for="checkbox">
    <span class="checkbox-image">checkbox</span>
    <span>동의합니다.</span>
  </label>
</div>
```

#### css

```css
.checkbox-wrap #checkbox {
  position: absolute;
  left: -9999px;
}
.checkbox-wrap label {
  cursor: pointer;
}
.checkbox-wrap label span {
  display: inline-block;
}
.checkbox-wrap .checkbox-image {
  width: 16px;
  height: 16px;
  border: 1px solid gray;
}
```

위와 같은 식으로 `input[type=checkbox]`를 absolute로 적용해서 보이지 않게 치운 후 체크박스(처럼 보이게 할) 엘리먼트에 체크박스 디자인의 css를 적용한다.

여기서 주의할 점은 absolute를 적용한 `input[type=checkbox]`를 안보이게 하기 위해 `top: -9999px`을 적용하면 IE 9-에서 체크박스 클릭 시 스크롤이 맨위로 이동한다.

top 값은 빼주어야 한다.
