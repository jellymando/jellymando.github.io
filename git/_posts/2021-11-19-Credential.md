---
layout: post
title: "[Windows] git 자격 증명 등록"
sitemap: false
---

{:toc .large-only}

## 주저리

[SSH 키 생성하고 Github에 추가하기](https://jellymando.github.io/git/2021-11-17-ssh/) 포스트에서 해결하지 못했던 문제를 해결했다.

윈도우에서 `git push`를 할 때 Authentication failed 에러가 났었는데,

```bash
git config --global --unset credential.helper
```

다른 문제를 해결하려고 위 명령어로 git credential을 지워버려서 그런 것 같다.

## 자격 증명 수정/추가

Mac은 모르겠으나, 윈도우에서는 제어판의 `Windows 자격 증명` 메뉴로 들어간다.

`일반 자격 증명` 목록에서 `git:https://github.com` 항목의 `편집`을 누른다.

`암호` 입력란에 github에서 발급받은 accessToken 값을 집어넣는다.

만약 `git:https://github.com` 항목을 삭제했다면, **일반 자격 증명 추가**를 클릭해 새로 추가한다.

~~`Windows 자격 증명 추가` 눌렀다가 안돼서 SSH 발급받았었건만..~~

## 참고사이트

[[Git] 토큰 인증 로그인 + 자격 증명](https://firstquarter.tistory.com/entry/Git-%ED%86%A0%ED%81%B0-%EC%9D%B8%EC%A6%9D-%EB%A1%9C%EA%B7%B8%EC%9D%B8-remote-Support-for-password-authentication-was-removed-on-August-13-2021-Please-use-a-personal-access-token-instead)<br/>
[Git, Pull/Push할 때 id password 묻지 않게 하기](https://pinedance.github.io/blog/2019/05/29/Git-Credential)
