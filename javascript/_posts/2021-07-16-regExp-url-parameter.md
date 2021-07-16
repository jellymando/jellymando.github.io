---
layout: post
title: "정규식을 이용하여 url에서 특정 parameter 값 자르기"
sitemap: false
---

{:toc .large-only}

### 정규식을 이용하여 url에서 특정 parameter 값 자르기

```js
url.match(/&parameter=([^&]*)/g).join("");

// &parameter=default&parameter=help
```

### 정규식 해석

- `&parameter=` 를 포함한 문자
- `[^` : ^가 꺽쇠안에 있으면 부정의 뜻, 괄호 내부에 포함되지 않은 문자 검색
- `[^&]` : &이 아닌 문자 검색
- `*` : 앞의 표현식이 0회 이상 연속으로 반복되는 부분 검색, **입력 안하면 한 글자만 뽑힘**

<br/>

[정규식으로 URL 쿼리스트링에서 특정 파라미터 추출](https://lovemewithoutall.github.io/it/URLSearchParams-on-IE/)<br/>
[](http://todactodac.blogspot.com/2018/12/javascript-python-url-parameter-ver.html)
[[자바스크립트] 동일한 단어를 문자열에서 찾기, Match() 함수](<https://webisfree.com/2014-11-28/[%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8]-%EB%8F%99%EC%9D%BC%ED%95%9C-%EB%8B%A8%EC%96%B4%EB%A5%BC-%EB%AC%B8%EC%9E%90%EC%97%B4%EC%97%90%EC%84%9C-%EC%B0%BE%EA%B8%B0-match()-%ED%95%A8%EC%88%98>)<br/>
[정규 표현식](https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Regular_Expressions#special-negated-character-set)
