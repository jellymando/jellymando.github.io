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
function initClient() {
  client = google.accounts.oauth2.initTokenClient({
    client_id: 'YOUR_CLIENT_ID',
    scope:
      'https://www.googleapis.com/auth/calendar.readonly \
                  https://www.googleapis.com/auth/contacts.readonly',
    callback: (tokenResponse) => {
      access_token = tokenResponse.access_token
    }
  })
}
function getToken() {
  client.requestAccessToken()
}
```

`client.requestAccessToken()` 함수 실행 시 로그인 팝업이 뜨고, 구글 계정으로 로그인하면 callback 함수가 실행된다.

## 리다이렉트 방식

팝업이 아닌 리다이렉트 방식을 사용해야 하는 경우 우선 승인 코드를 발급받아야 한다.

`google.accounts.oauth2.initCodeClient`로 client 객체를 생성한다.

```js
function initClient() {
  client = google.accounts.oauth2.initCodeClient({
    client_id: 'YOUR_CLIENT_ID',
    scope:
      'https://www.googleapis.com/auth/calendar.readonly \
                  https://www.googleapis.com/auth/photoslibrary.readonly',
    ux_mode: 'redirect',
    redirect_uri: 'YOUR_AUTHORIZATION_CODE_ENDPOINT_URI'
  })
}
// Request an access token
function getAuthCode() {
  // Request authorization code and obtain user consent
  client.requestCode()
}
```

`client.requestCode()` 함수 실행 시 승인 코드를 `redirect_uri` 파라미터로 전달받는다.

전달받은 승인 코드를 사용하여 액세스 토큰을 발급받을 수 있다.

```js
await axios.post(
  `https://oauth2.googleapis.com/token?code=${code}&client_id=${CLIENT_ID}&client_secret=${CLIENT_SECRET}&redirect_uri=postmessage&grant_type=authorization_code`,
  {},
  {
    headers: {
      'Content-Type': 'application/x-www-form-urlencoded'
    }
  }
)
```

이렇게 하면 응답 값으로 `access_token`이 넘어온다.

주의할 점은 `redirect_uri` 파라미터에 API Console에 저장한 리디렉션 URI이 아닌 'postmessage'를 입력해야 한다는 것이다.

리디렉션 URI를 입력하면 `redirect_uri_mismatch` 에러가 발생한다 ㅠ

## api 호출하기

발급받은 access token을 변수나 쿠키에 저장하여, 구글 인증이 필요한 api를 호출할 때 헤더의 `Authorization` 값에 담에 보낼 수 있다.

## 참고사이트

[OAuth 2.0 액세스 토큰 가져오기](https://developers.google.com/identity/protocols/oauth2/javascript-implicit-flow#obtainingaccesstokens)<br/>
[새로운 방법](https://developers.google.com/identity/oauth2/web/guides/migration-to-gis#implicit_flow_examples)<br/>
[코드 모델 사용](https://developers.google.com/identity/oauth2/web/guides/use-code-model)<br/>
[갱신 및 액세스 토큰의 승인 코드 교환](https://developers.google.com/identity/protocols/oauth2/web-server#httprest_3)<br/>
[Google OAuth 2 authorization - Error: redirect_uri_mismatch](https://stackoverflow.com/a/48121098)
