---
title: "[error] 기준 주소를 다시 지정하는 중에는 커밋 메시지를 변경할 수 없습니다."
categories: [GIT]
tags: [git, error]
---

{:toc .large-only}

vscode gitlens에서 커밋 하려고 하면 "기준 주소를 다시 지정하는 중에는 커밋 메시지를 변경할 수 없습니다. 기준 주소 다시 지정 작업을 완료하고, 대신 대화형 기준 주소 다시 지정을 사용하세요." 토스트 메세지가 뜬다.

아마도 다른 브랜치에서 `pull` 해오다 생긴 이슈인 것 같다.

아래 명령어를 입력하면 해결된다.

```js
rm -fr ".git/rebase-merge"
```
