---
layout: post
title: 'Transition vs Animation'
sitemap: false
---

{:toc .large-only}

## Transition

- 속도, 타이밍 함수, 딜레이 등을 사용자 지정하여 CSS 속성을 변경할 때 애니메이션처럼 보이게 함
- 자동으로 작동하지 않음 (hover나 onclick 같은 이벤트에 의해 동작)

```css
#delay1 {
  position: relative;
  transition-property: font-size;
  transition-duration: 4s;
  transition-delay: 2s;
  font-size: 14px;
}

#delay1:hover {
  transition-property: font-size;
  transition-duration: 4s;
  transition-delay: 2s;
  font-size: 36px;
}
```

### 단축 문법

```css
div {
  transition: <property> <duration> <timing-function> <delay>;
}
```

### Transition 완료 감지하기

```js
el.addEventListener('transitionend', updateTransition, true)
```

## Animation

- `@keyframes` 규칙을 사용하여 애니메이션 구현
- 속도, 타이밍 함수, 딜레이 사용자 지정 가능하며 중지, 중지 후 값, 반복 횟수 등도 지정 가능
- 자동으로 작동시킬 수 있음

```css
p {
  animation-duration: 3s;
  animation-name: slidein;
}

@keyframes slidein {
  from {
    margin-left: 100%;
    width: 300%;
  }

  to {
    margin-left: 0%;
    width: 100%;
  }
}
```

## 차이점

- Transition은 하나의 시작 상태에서 끝 상태로 변경하는 반면 Animation은 많은 중간 상태들로 구성 가능
- Transition은 이벤트가 발생해야 작동하지만 Animation은 바로 작동시킬 수 있다.
- Animation이 Transition 보다 더 많은 애니메이션 옵션을 설정할 수 있음

## 정리

- 단순한 애니메이션 효과를 주고 싶다면 Transition을 사용하는 것이 효율적이다.
- 복잡한 애니메이션을 구현하거나 페이지가 로드될 때 애니메이션을 실행해야 할 때는 Animation을 사용한다.

## 참고사이트

[Transitions vs Animations](https://cssanimation.rocks/transition-vs-animation/)<br/>
[[CSS] 트랜지션(Transition)과 애니메이션(Animation)](https://ahribori.com/article/5a0c49926c9eef13d882e3ea)<br/>
[CSS 트랜지션 사용하기](https://developer.mozilla.org/ko/docs/Web/CSS/CSS_Transitions/Using_CSS_transitions)<br/>
[CSS 애니메이션 사용하기](https://developer.mozilla.org/ko/docs/Web/CSS/CSS_Animations/Using_CSS_animations)
