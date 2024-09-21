---
title: "[MongoDB] Schema 스키마 타입 제외 속성들"
categories: [BACKEND]
tags: [mongodb]
---

{:toc .large-only}

## mongoose 스키마의 다양한 속성

| Name        | Description                             |
| ----------- | --------------------------------------- |
| `required`  | 꼭 입력해야 한다.                       |
| `unique`    | 다른 행과 중복되면 안 된다.             |
| `trim`      | 공백을 제거합니다.(문자열 타입에 사용)  |
| `default`   | 문서가 생성되면 기본값으로 저장됩니다.  |
| `lowercase` | 대문자를 소문자로 저장한다(문자열 타입) |
| `match`     | 정규식으로 저장하려는 값과 비교한다.    |
| `validate`  | 함수로 개발자가 조건을 만듭니다.        |
| `set`       | 값을 입력할 때 함수로 조건을 만듭니다.  |
| `get`       | 값을 출력할 때 함수로 조건을 만듭니다.  |
| `ref`       | 해당하는 모델을 참조할 때 사용한다.     |

<br/>

```js
const exampleSchema = mongoose.Schema({
   firstName: {
    type: String,
    required: true,
    trim: true,
    lowercase: true
   },
   lastName:{
    type: String,
    trim: true,
    lowercase: true
   }
   age:{
    type: Number,
    required: true,
   }
   created:{
    type: Date,
    default: Date.now
   },
   number:{
    type: Number,
    match: /^\d{3}-\d{3,4}-\d{4}$/
   },
   password:{
    type: String,
    validate: [
      function(password) {
       return password && password.length>6;
      }, '비밀번호를 입력하거나 길이가 6보다 커야합니다.'
     ]
   },
   author:{
    type: Schema.Types.Id,
    ref: 'User'
   }
});
```

<br/>

[web_server node mongoose 스키마 타입 속성 메서드](https://m.blog.naver.com/rwans0397/220696586520)
