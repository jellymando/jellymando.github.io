---
title: "fast-forward merge 커밋 메시지 생성하기"
categories: [GIT]
tags: [git]
---

{:toc .large-only}

## Merge 했을 때 커밋 메시지가 생성되지 않는 경우

다른 브랜치를 머지했는데 git 로그에 merge 되었다는 커밋 메시지는 생성되지 않고, 다른 브랜치의 커밋 내역만 생성되었다.

하지만 커밋 내역들이 머지해서 가져온 것이라는 티를 내줘야 할 것 같아서, 머지 메시지 생성 옵션에 대해 알아보게 되었다.

## fast-forward

2개의 커밋 A와 B가 있을 때, A의 히스토리가 B의 히스토리에 전부 포함되어 있는 경우, 2개의 커밋은 **fast-forward** 관계이다.

<img src="/assets/img/blog/2022-04-06-merge-message_01.png" style="margin-bottom:30px;">

위 그림에서 bugfix는 master 브랜치에서 분기한 브랜치다.

bugfix 브랜치를 master 브랜치로 병합할 때, master 브랜치의 상태는 bugfix 이후로 변경되지 않았다.

때문에 bugfix 브랜치는 master 브랜치의 이력을 모두 포함하고 있어서 fast-forward merge가 된다.

이렇게 fast-forward merge인 경우에는 머지 커밋 생성되지 않는다.

<img src="/assets/img/blog/2022-04-06-merge-message_02.png">

## non fast-forward merge

병합 실행 시에 fast-forward merge인 경우라도 non fast-forward merge 옵션을 지정하면 머지 커밋을 생성할 수 있다.

non fast-forward를 줄여서 --no-ff 라고 한다.

#### 한 번만 --no-ff

```bash
git merge --no-ff 브랜치명
```

#### 모든 브랜치에서 항상 --no-ff

```bash
git config branch.autosetuprebase always
```

#### 특정 브랜치에서 항상 --no-ff

```bash
git config branch.<name>.rebase true
```

#### 알리아스를 이용하여 --no-ff

```bash
git config --global alias.nffmerge "merge --no-ff"

git nffmerge
```

## 참고사이트

[도식으로 보는 git-merge의 --ff, --no-ff, --squash의 차이점](https://blog.naver.com/PostView.nhn?blogId=parkjy76&logNo=220308638231&categoryNo=73&parentCategoryNo=0&viewDate=&currentPage=1&postListTopCurrentPage=1&from=postView)<br/>
[브랜치 통합하기](https://backlog.com/git-tutorial/kr/stepup/stepup1_4.html)
