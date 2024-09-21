---
title: "[Inquirer] 커맨드 라인에 Prompts 설정하기"
categories: [node]
tags: [node]
---

{:toc .large-only}

### Inquirer 설치

```bash
npm i inquirer
```

### Prompt 생성

js 파일 생성 후 아래 코드 입력

```js
const inquirer = require("inquirer");
inquirer
  .prompt([
    {
      name: "faveReptile",
      message: "What is your favorite reptile?",
      default: "Alligators",
    },
  ])
  .then((answers) => {
    console.info("Answer:", answers.faveReptile);
  });
```

<br/>

`prompt`를 설정하여 멀티로 만들거나 선택지를 추가할 수 있다.

```js
inquirer
  .prompt([
    {
      name: "faveReptile",
      message: "What is your favorite reptile?",
      default: "Alligators",
    },
    {
      name: "faveColor",
      message: "What is your favorite color?",
      default: "#008f68",
    },
  ])
  .then((answers) => {
    console.info("Answers:", answers);
  });
```

```js
inquirer
  .prompt([
    {
      type: "rawlist",
      name: "reptile",
      message: "Which is better?",
      choices: ["alligator", "crocodile"],
    },
  ])
  .then((answers) => {
    console.info("Answer:", answers.reptile);
  });
```

<br/>

[How To Create Interactive Command-line Prompts with Inquirer.js](https://www.digitalocean.com/community/tutorials/nodejs-interactive-command-line-prompts)
