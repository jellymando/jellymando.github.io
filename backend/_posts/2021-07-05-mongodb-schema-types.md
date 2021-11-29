---
layout: post
title: "[MongoDB] Schema 스키마 타입 속성"
sitemap: false
---

{:toc .large-only}

```js
const exampleSchema = new mongoose.Schema({
   name:{
    type: String,
    required: true
   }
   age: Number
   number:Schema.Types.ObjectId
   created: {
    type: Date,
    default: Date.now
   }
   binary: Buffer,
   living: Boolean
   mixed: Schema.Types.Mixed
   array: [],
   arrayNumber: [Number],
   arrayString: [String]
});
```

<br/>

[web_server node mongoose 스키마 타입 속성 메서드](https://m.blog.naver.com/rwans0397/220696586520)
