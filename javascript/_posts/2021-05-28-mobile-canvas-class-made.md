---
layout: post
title: "Mobile Canvas🎨 클래스 만들기🖌"
sitemap: false
---

{:toc .large-only}

## Why?

VP에서 simple-canvas 라이브러리를 사용하던 중 에러 발생.

(ios 터치 좌표 안맞음 등)

모바일 브라우저에서 문제 없이 작동하는 심플한 Painter 클래스를 만들기로 함.

## How?

- React + TypeScript
- EventEmitter
- EventListener

## Constructor

- canvas (html canvas element)
- ctx
- isDrawing (mousedown 여부)
- strokeColor
- thickness
- removeDrawEvent (removeEventListener method)

## Method

### setTarget

렌더링 후 canvasRef.current가 생성되면 Painter에 캔버스 엘리먼트를 전달해준다.

캔버스 엘리먼트로 ctx를 만든다.

### addDrawEvent

EventListner들을 추가한다.

### removeDrawEvent

컴포넌트가 언마운트 될 때 실행할 메서드.

EventListner들을 제거한다.

### drawStart

isDrawing을 true로 바꾸고, color와 두께를 설정한다.

### draw

position 파라미터를 받아 실제로 canvas에 그림을 그린다.
