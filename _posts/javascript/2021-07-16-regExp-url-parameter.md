---
title: '정규식을 이용하여 URL 체크하기 + 정규식 사용법 정리'
categories: [JAVASCRIPT]
tags: [javascript, 정규식]
---

{:toc .large-only}

## 유효한 URL 체크하기

```js
const urlRex = /https?:\/\/[\w\-\.]+/
```

- `https?` : http를 포함하고 s는 있거나 없음
- `\/\/` : //
- `[\w\-\.]+` : \w(영문자, 언더스코어), 하이픈(-), 쩜(.) 으로 이루어진 문자열이 한개 이상(+) 있움

아래 예시 url에서 밑줄 친 부분이 정규식으로 체크된다.

<u>https://about.google</u>:443/products/

### 포트번호 체크하기

url에서 포트번호까지 포함시키고 싶다면 `(:\d+)?`을 추가하면 된다.

```js
const urlRex = /https?:\/\/[\w\-\.]+(:\d+)?/
```

아래 예시 url에서 밑줄 친 부분이 정규식으로 체크된다.

<u>https://about.google:443</u>/products/

## 캐릭터 클래스

문자 종류를 구분할 수 있는 패턴이다.

플래그가 소문자면 일치, 대문자면 일치하지 않음을 의미한다.

| 플래그 | 설명                      | 예시                                               |
| ------ | ------------------------- | -------------------------------------------------- |
| \d     | 0-9 까지의 숫자           | ex) `\d{2,3}` : 숫자 2개 이상 3개 이하             |
| \D     | 0-9 까지의 숫자가 아닌 것 | ex) `\D{2,3}` : 숫자가 아닌 문자 2개 이상 3개 이하 |
| \w     | 문자 혹은 언더바          | `A-Za-z0-9_`와 일치                                |
| \W     | `\w`가 아닌 것            |                                                    |

## 참고사이트

[[JS] 📚 정규표현식(RegExp) - 이해하기 쉽게 정리 + 응용 예제](https://inpa.tistory.com/entry/JS-%F0%9F%93%9A-%EC%A0%95%EA%B7%9C%EC%8B%9D-RegExp-%EB%88%84%EA%B5%AC%EB%82%98-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-%EC%89%BD%EA%B2%8C-%EC%A0%95%EB%A6%AC)<br/>
[JavaScript 문자열이 유효한 URL인지 확인하는 방법](https://www.freecodecamp.org/news/check-if-a-javascript-string-is-a-url/)<br/>
[정규 표현식](https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Regular_Expressions#special-negated-character-set)<br/>
[Character classes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions/Character_Classes)
