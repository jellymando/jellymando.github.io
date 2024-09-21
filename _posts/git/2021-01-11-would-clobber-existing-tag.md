---
title: "[error] 거부됨 - would clobber existing tag"
categories: [GIT]
tags: [git, error]
---

{:toc .large-only}

## ! [거부됨] v0.7.62 -> v0.7.62 (would clobber existing tag)

yarn install 시 위와 같은 에러가 뜸.<br/>

[SourceTree에서 푸시를 시도 할 때 "태그가 이미 존재하기 때문에 업데이트가 거부되었습니다."](https://qastack.kr/programming/31929667/updates-were-rejected-because-the-tag-already-exists-when-attempting-to-push-i)<br/>

git pull --tags -f 도 하고 여러가지 해봤지만 똑같다..

캐쉬 삭제를 하고 나서 install하니 잘 된다.

```js
yarn cache clean
```
