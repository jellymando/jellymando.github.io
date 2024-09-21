---
title: "[MongoDB] 설치하기"
categories: [BACKEND]
tags: [mongodb]
---

{:toc .large-only}

## Mongoose 설치

```js
npm install mongoose
```

## mongodb 연동

## Schema 생성

models 폴더를 만든 후 스키마 파일을 생성한다.

```js
// Item.js
const mongoose = require("mongoose");
cosnt Schema= mongoose.Schema;

const itemSchema = new mongoose.Schema({
  title: {
    type: String,
    required: true,
  },
});

const Item = mongoose.model("Item", itemSchema);

module.exports = Item;
```

## Router 생성

```js
const Item = require("../models/Item");

module.exports = function (app) {
  app.get("/", function (req, res) {
    res.render("index.html");
  });

  app.post("/items", (req, res) => {
    const item = new Item(req.body);
    item.save((err, doc) => {
      if (err) return res.json({ success: false, err });
      return res.status(200).json({ success: true });
    });
  });

  app.get("/items", (req, res) => {
    Item.find((err, data) => {
      if (err) return res.status(500).send({ error: "database failure" });
      res.json(data);
    });
  });
};
```

<br/>
> 주의사항 : 라우터를 참조하기 전에 body-parser를 먼저 참조해야 한다.
