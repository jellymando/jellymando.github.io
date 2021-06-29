---
layout: post
title: "border-width를 이용한 가운데 뚫린 배경 만들기⭕️"
sitemap: false
---

{:toc .large-only}

바코드 리더 UI 개발중 가운데가 네모낳게 뚫린 배경을 어떻게 만들어야할지 고민해보았다.

`background` 속성으로는 가운데를 제외하고 배경을 적용할 수 없었기에 `border`를 사용해야 했다.

더군다나 가운데 뚫린 부분은 반응형으로 크기가 고정되어 있지 않기 때문에 `min()`, `max()`를 사용했다.

```css
border-width: 상하 좌우;
```

가운데 뚫린 부분을 정사각형 박스라고 치고, 박스의 width, height는 60vw, 최대 216px로 정한다.

`$qrWidth`(좌우), `$qrHeight`(상하) 변수를 만든다. (`scss`로 개발했다)

`border-width` 속성의 값은 상하, 좌우이기 때문에 각각 50vh, 50vw에서 박스 width(=height)의 1/2를 빼야한다.

박스의 `width/2`는 `max(30vw, 108px)` 이므로 여기서 50vw를 빼면 `$qrWidth`는 `calc(max(20vw, 50vw - 108px))`

박스의 최대값이 정해져 있고 반응형으로 했을 때 계속 작아지는게 가능하니 `$qrWidth`가 최대값이 나올 수 있도록 `max()`를 사용한다.

`$qrHeight` 또한 최대값이 나오게 하려면 50vh에서 빼는 숫자가 작을수록 크게 나오므로 `calc(50vh - min(30vw, 108px))`

```scss
$qrWidth: calc(max(20vw, 50vw - 108px));
$qrHeight: calc(50vh - min(30vw, 108px));
```

<br/>

또 한가지, `border-width`를 적용한 엘리먼트에 `width: 100vw; height: 100vh`를 적용해야 한다.

모바일일 경우 `height: 100vh` 적용하면 페이지를 넘어가기 때문에 아래 포스트를 참조하여 위로 땡겨준다.

[모바일에서 100vh 값이 100%보다 커서 페이지 밖으로 빠져나갈 때](https://jellymando.github.io/css/2021-06-29-100vh-with-mobile/)
