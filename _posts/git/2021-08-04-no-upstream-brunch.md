---
title: "[error] The current branch master has no upstream branch"
categories: [Git]
tags: [git, error]
---

{:toc .large-only}

```js
fatal: The current branch <branchname> has no upstream branch.
To push the current branch and set the remote as upstream, use

git push --set-upstream origin <branchname>
```

`push` 할 때 브랜치에 상향 분기가 없다고 나오는 에러.

`git push --set-upstream origin <branchname>`을 직접 치라고 나옴.

오류의 원인은 로컬 분기에서 원격 분기를 항상 생성하도록 하지 않았기 때문.

아래 명령어 입력하여 해결

```js
git config --global push.default current
```

<br/>

[How to Fix Git fatal: The current branch has no upstream branch](https://vancelucas.com/blog/how-to-fix-git-fatal-the-current-branch-has-no-upstream-branch/)
