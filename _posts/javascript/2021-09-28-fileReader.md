---
title: "input과 fileReader로 file 업로드하고 읽기"
categories: [JAVASCRIPT]
tags: [javascript, file]
---

{:toc .large-only}

## 마크업

우선 input 태그를 사용해 파일을 업로드 해보자.

```js
<InputFile
    ref={inputFile}
    type="file"
    onChange={(e) => handleImportChange(e)}
/>
<Button onClick={handleImportClick}>Import</Button>
```

`InputFile` 컴포넌트에는 `display: none;` 스타일을 적용하여 보이지 않도록 했다.

`Button`을 클릭하면 `InputFile`이 클릭되도록 하고, `InputFile`에 `onchange` 이벤트를 등록한다.

## file 전달

file의 트리 경로는 `event.target.files[0]`이다.

fili은 객체로서 name, size, type 값을 가지고 있다.

type은 MEME 타입 값이다. [Common MIME types](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types/Common_types)

```js
const handleImportChange = (e) => {
  const file = e.target.files[0];
  console.log("file", file);
};
```

## FileReader()

`FileReader` 인스턴스를 생성한다.

`onload` 메서드로 result 값을 얻을 수 있다.

`readAsText` 메서드로 파일의 컨텐츠를 읽을 수 있다.

```js
const handleImportChange = (e) => {
  const file = e.target.files[0];
  const reader = new FileReader();
  reader.onload = function (e) {
    console.log(e.target.result);
  };
  // 혹은
  reader.onload = function () {
    console.log(reader.result);
  };
  reader.readAsText(file);
};
```

## json 파일 파싱

file의 타입이 json이라면 파싱해준다.

```js
const handleImportChange = (e) => {
  const file = e.target.files[0];
  const reader = new FileReader();
  reader.onload = function (e) {
    console.log(e.target.result);
  };
  // 혹은
  reader.onload = function () {
    console.log(JSON.parse(reader.result));
  };
  reader.readAsText(file);
};
```

## 참고사이트

[input type="file"](https://developer.mozilla.org/ko/docs/Web/HTML/Element/Input/file)<br/>
[FileReader.onload](https://developer.mozilla.org/en-US/docs/Web/API/FileReader/onload)<br/>
[FileReader](https://developer.mozilla.org/ko/docs/Web/API/FileReader)
