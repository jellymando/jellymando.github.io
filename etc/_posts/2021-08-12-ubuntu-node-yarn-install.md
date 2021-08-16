---
layout: post
title: "[ubuntu] git, node.js, yarn 설치하기"
sitemap: false
---

{:toc .large-only}

### git 설치

```bash
sudo apt install git
```

### 버전 확인

```bash
git --version
```

### node.js 설치

```bash
sudo apt-get update
sudo apt-get install -y build-essential
sudo apt-get install curl
```

<br/>

[이 링크](https://github.com/nodesource/distributions#installation-instructions)에서 node 버전 확인 후 아래 명령어에서 원하는 버전 입력

```bash
curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash --
sudo apt-get install -y node.js
```

### 버전 확인

```bash
node -v
npm -v
```

### Yarn 설치

```bash
sudo npm install -g yarn
```

### 버전 확인

```bash
yarn -v
```

<br/>

[[Linux] 우분투 Git 설치 / 다운로드 & 사용 방법](https://coding-factory.tistory.com/502)<br/>
[[Ubuntu] 우분투에 Nodejs와 Yarn 설치](https://blog.system32.kr/205)
