---
title: "Git checkout 👉 switch & restore"
categories: [Git]
tags: [git]
---

{:toc .large-only}

Git 2.23 부터 checkout의 기능이 switch와 restore로 분리되었다.

- **checkout** : Switch branches or restore working tree files
- **switch**: Switch branches
- **restore**: Restore working tree files

<br/>
[참고사이트](https://blog.outsider.ne.kr/1505)
<br/>

## switch

branch를 변경한다.

```js
git switch develop
```

branch를 생성하고 해당 브런치로 변경한다.

```js
git switch -c new-branch
```

<br/>
[Git 공식 문서 - switch](https://git-scm.com/docs/git-switch)

## restore

작업중인 파일을 복원한다.

```js
git restore hello.c
```

색인에서 HEAD의 버전과 일치하도록 파일을 복원 (git-reset[1]을 사용하는 것과 동일함)

```js
git restore --staged hello.c
```

<br/>
[Git 공식 문서 - restore](https://git-scm.com/docs/git-restore)
