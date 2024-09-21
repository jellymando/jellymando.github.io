---
title: '구글 인증 후 access token 발급받기..'
categories: [JAVASCRIPT]
tags: [javascript]
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

access token을 발급받는 방법에는 **암시적 권한 모델**을 사용하는 방법과 **승인 코드 모델**을 사용하는 방법이 있다.

혹은 직접 OAuth2 URL에 파라미터를 입력하여 접속하여 리다이렉트 하는 방법도 있다.

access token을 발급받는 방식은 팝업으로 인증한 후 callback 함수를 통해 토큰 값을 얻거나, 리다이렉트로 인증한 후 URI에 승인 코드를 전달해주는 방식이 있다.

### 암시적 권한 모델

암시적 권한 모델은 구글 라이브러리를 사용하여 엑세스 토큰을 바로 얻을 수 있다.

해당 모델은 보안 문제로 인해 <u>팝업 UX만 지원</u>한다.

암시적 권한 모델에서는 `initTokenClient` 메서드로 client 객체를 생성하고 `requestAccessToken` 메서드로 엑세스 토큰을 요청한다.

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

`requestAccessToken` 함수 실행 시 로그인 팝업이 뜨고, 구글 계정으로 로그인하면 callback 함수를 통해 `access_token` 값이 넘어온다.

### 승인 코드 모델

승인 코드 모델은 구글로부터 승인 코드를 받고, 해당 승인 코드를 엑세스 토큰으로 교환하는 방법이다.

팝업이나 리다이렉트 UX를 통해 승인 코드를 얻을 수 있다.

승인 코드 모델에서는 `initCodeClient` 메서드로 client 객체를 생성하고 `requestCode` 메서드로 승인 코드를 요청한다.

#### 팝업 UX

```js
function initClient() {
  client = google.accounts.oauth2.initCodeClient({
    client_id: 'YOUR_CLIENT_ID',
    scope: 'https://www.googleapis.com/auth/calendar.readonly',
    ux_mode: 'popup',
    callback: (response) => {
      const xhr = new XMLHttpRequest()
      xhr.open('POST', code_receiver_uri, true)
      xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded')
      // Set custom header for CRSF
      xhr.setRequestHeader('X-Requested-With', 'XmlHttpRequest')
      xhr.onload = function () {
        console.log('Auth code response: ' + xhr.responseText)
      }
      xhr.send('code=' + code)
    }
  })
}
function getAuthCode() {
  client.requestCode()
}
```

`requestCode` 함수 실행 시 로그인 팝업이 뜨고, 구글 계정으로 로그인하면 callback 함수를 통해 승인 코드 값이 넘어온다.

#### 리다이렉트 UX

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
function getAuthCode() {
  client.requestCode()
}
```

`crequestCode` 함수 실행 시 승인 코드를 `redirect_uri`로 리다이렉트 되며 파라미터로 승인 코드를 전달받는다.

#### 승인 코드로 엑세스 토큰 교환

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

`oauth2.googleapis.com/token`로 승인 코드 외 필수 값을 POST로 보내면 응답 값으로 access_token 값이 넘어온다.

팝업 UX로 승인 코드를 받은 경우 `redirect_uri` 파라미터에 리디렉션 URI를 입력하면 에러가 나서 'postmessage'를 입력했다.

### OAuth2 URL을 직접 열어 승인 코드 or 토큰 얻기

```js
// 승인 코드
const accountsUrl = `https://accounts.google.com/o/oauth2/v2/auth?scope=${encodeURIComponent(
  SCOPES
)}&access_type=offline&include_granted_scopes=true&response_type=code&redirect_uri=${encodeURIComponent(
  uri
)}&client_id=${CLIENT_ID}`

// 토큰
const accountsUrl2 = `https://accounts.google.com/o/oauth2/v2/auth?scope=${encodeURIComponent(
  SCOPES
)}&access_type=online&include_granted_scopes=true&response_type=token&redirect_uri=${encodeURIComponent(
  uri
)}&client_id=${CLIENT_ID}`

window.open(accountsUrl)
```

`response_type`에 따라 승인 코드나 토큰을 얻을 수 있다.

- `&response_type=code&access_type=offline` 값을 보내면 uri에 파라미터로 승인 코드가 넘어온다.
- `&response_type=token&access_type=online` 값을 보내면 uri에 anchor(#)가 붙어서 access_token 값이 넘어온다.

## 참고사이트

[OAuth 2.0 액세스 토큰 가져오기](https://developers.google.com/identity/protocols/oauth2/javascript-implicit-flow#obtainingaccesstokens)<br/>
[새로운 방법](https://developers.google.com/identity/oauth2/web/guides/migration-to-gis#implicit_flow_examples)<br/>
[코드 모델 사용](https://developers.google.com/identity/oauth2/web/guides/use-code-model)<br/>
[갱신 및 액세스 토큰의 승인 코드 교환](https://developers.google.com/identity/protocols/oauth2/web-server#httprest_3)<br/>
[Google OAuth 2 authorization - Error: redirect_uri_mismatch](https://stackoverflow.com/a/48121098)<br/>
[인증 URI 매개변수](https://developers.google.com/identity/openid-connect/openid-connect?hl=ko#authenticationuriparameters)<br/>
[OAuth 2.0 암시적 권한 부여 유형이란 무엇입니까?](https://developer.okta.com/blog/2018/05/24/what-is-the-oauth2-implicit-grant-type)
