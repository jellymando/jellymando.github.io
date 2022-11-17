---
layout: post
title: '구글 인증 access token 발급받고 api 호출하기'
sitemap: false
---

{:toc .large-only}

## 기존 방식

기존에는 `gapi.auth2`나 `gapi.client`를 통해 인증을 받을 수 있었지만 앞으로 지원이 중단되어 아래와 같이 `gapi.client.init` 호출 시 새로운 라이브러리를 사용하라는 오류 메시지가 나온다.

```js
gapi.client.init({
  apiKey: 'YOUR_API_KEY',
  clientId: 'YOUR_CLIENT_ID',
  discoveryDocs: [discoveryUrl],
  scope: SCOPE
})
```

## 새로운 방식

새로운 인증 방식에서는 `google.accounts.oauth2.initTokenClient`로 client 객체를 생성한다.

```js
client = google.accounts.oauth2.initTokenClient({
  client_id: 'YOUR_CLIENT_ID',
  scope:
    'https://www.googleapis.com/auth/calendar.readonly \
                  https://www.googleapis.com/auth/contacts.readonly',
  callback: (tokenResponse) => {
    access_token = tokenResponse.access_token
  }
})
```

위 함수 실행 시 로그인 팝업이 뜨고, 구글 계정으로 로그인하면 callback 함수가 실행된다.

## api 호출하기

발급받은 access token을 변수나 쿠키에 저장하여, 구글 인증이 필요한 api를 호출할 때 헤더의 Authorization 값에 담에 보낼 수 있다.

## 참고사이트

[OAuth 2.0 액세스 토큰 가져오기](https://developers.google.com/identity/protocols/oauth2/javascript-implicit-flow#obtainingaccesstokens)<br/>
[새로운 방법](https://developers.google.com/identity/oauth2/web/guides/migration-to-gis#implicit_flow_examples)
