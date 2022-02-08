---
layout: post
title: 'css animation 여러개 실행시키기'
sitemap: false
---

{:toc .large-only}

## When

한 엘리먼트에 여러개의 css 애니메이션을 <u>각각</u> 적용해야 할 경우

(각각 적용할 필요가 없다면 하나의 애니메이션 안에서 모든 효과를 적용하면 된다.)

## How

`,` 쉼표를 사용하여 여러개의 애니메이션을 적용할 수 있다.

주의할 점은 하나의 애니메이션을 실행할 때와 멀티 애니메이션의 css 프로퍼티 순서가 다르다는 것이다.

#### Single Animation

```css
animation: 0.5s ease-in ${fadeInOut};
```

#### Multiple Animation

```css
animation: ${fadeIn} 0.5s ease-in forwards,
        ${fadeOut} 0.8s ease-in 0.5s forwards;
```

위와 같이 작성하면, fadeIn이 0.5초 동안 **실행된 후** fadeOut이 0.8초 동안 실행된다.

fadeOut 애니메이션에 delay 값을 넣었기 때문이다.

delay 값을 빼면 두 애니메이션이 동시에 실행된다.

## 참고사이트

[Using two animations on one element, CSS](https://stackoverflow.com/questions/37428067/using-two-animations-on-one-element-css)
