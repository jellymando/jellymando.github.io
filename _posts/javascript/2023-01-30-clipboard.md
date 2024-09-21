---
title: 'Clipboard API 사용하기'
categories: [Javascript]
tags: [javascript, clipboard]
---

{:toc .large-only}

## Clipboard API

Clipboard API는 시스템 클립보드에 데이터를 읽거나 쓸 수 있는 **비동기** API이다.

아래 메서드를 포함한다.

### read()

클립보드에서 이미지 등의 데이터를 가져온다.

```js
const clipboardContents = await navigator.clipboard.read()

for (const item of clipboardContents) {
  if (!item.types.includes('image/png')) {
    throw new Error('Clipboard contains non-image data.')
  }
  const blob = await item.getType('image/png')
  destinationImage.src = URL.createObjectURL(blob)
}
```

### readText()

클립보드에서 문자열 텍스트를 가져온다.

```js
navigator.clipboard
  .readText()
  .then((clipText) => (document.getElementById('outbox').innerText = clipText))
```

### write()

클립보드에 이미지와 같은 임의의 데이터를 쓴다.

`data`는 클립보드에 기록할 데이터가 포함된 객체 배열이다.

```js
function setClipboard(text) {
  const type = 'text/plain'
  const blob = new Blob([text], { type })
  const data = [new ClipboardItem({ [type]: blob })]

  navigator.clipboard.write(data).then(
    () => {
      /* success */
    },
    () => {
      /* failure */
    }
  )
}
```

### writeText()

클립보드에 문자열 텍스트를 쓴다.

```js
navigator.clipboard.writeText('<empty clipboard>').then(
  () => {
    /* clipboard successfully set */
  },
  () => {
    /* clipboard write failed */
  }
)
```

### permission

Clipboard API를 사용하기 위해서는 `clipboard-read` 혹은 `clipboard-write` API 권한이 필요하며,

이 권한은 Permissions API를 통해 체크하거나 취소할 수 있다.

```js
navigator.permissions.query({ name: 'clipboard-write' }).then((result) => {
  console.log('result.state', result.state)
})
```

## 참고사이트

[Clipboard](https://developer.mozilla.org/ko/docs/Web/API/Clipboard)
