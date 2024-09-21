---
title: '[cherry-pick] 특정 커밋만 merge 하기'
categories: [Git]
tags: [git]
---

{:toc .large-only}

## cherry-pick

다른 브랜치의 특정 커밋을 가져오는 명령어

브랜치의 모든 커밋을 merge하지 않고 특정 커밋만 가져오고 싶을 때 사용

## 사용법

```bash
git cherry-pick [commit id] // 커밋 내용을 가져온 후 새로운 커밋 생성
git cherry-pick -n [commit id] // 커밋 내용만 가져옴
```

## 참고사이트

[git cherry-pick : 특정 commit만 반영하기](https://donggov.tistory.com/32)
