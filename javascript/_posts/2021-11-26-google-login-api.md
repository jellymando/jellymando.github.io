---
layout: post
title: "구글 로그인 api 연동하기"
sitemap: false
---

{:toc .large-only}

## 인증 자격 증명 만들기

1. [사용자 인증 정보](https://console.developers.google.com/apis/credentials) 페이지로 이동한다.
1. [[자바스크립트] 구글 로그인 API 쉽게 구현 방법 및 예제- OAuth 2.0, Javascript, Jsp](https://tyrannocoding.tistory.com/51) 를 참고하여 <u>동의 화면 구성, API 키, OAuth 클라이언트 ID를 생성한다.

## Google Platform 라이브러리 로드

Google 로그인을 연동할 html 문서에 Google Platform 라이브러리를 로드한다.

```html
<script src="https://apis.google.com/js/platform.js" async defer></script>
```

## 메타태그에 클라이언트 ID 지정

`google-signin-client_id` 메타태그에 클라이언트 ID를 입력한다.

```html
<meta
  name="google-signin-client_id"
  content="YOUR_CLIENT_ID.apps.googleusercontent.com"
/>
```

## 로그인 버튼 추가

구글에서 제공하는 기본 로그인 버튼을 넣으려면 `div` 태그에 `g-signin2` 클래스명을 추가한다.

```html
<div class="g-signin2" data-onsuccess="onSignIn"></div>
```

<img src="/assets/img/blog/2021-11-26-google-people-api.png" style="margin-top:30px">

## 프로필 정보 얻기

기본 양식을 사용하여 Google에 사용자로 로그인 한 후 사용자의 Google ID, 이름, 프로필 URL 및 이메일 주소에 액세스 할 수 있다.

사용자의 프로필 정보를 검색하려면 `getBasicProfile()` 메서드를 사용한다.

```js
function onSignIn(googleUser) {
  var profile = googleUser.getBasicProfile();
  console.log("ID: " + profile.getId()); // Do not send to your backend! Use an ID token instead.
  console.log("Name: " + profile.getName());
  console.log("Image URL: " + profile.getImageUrl());
  console.log("Email: " + profile.getEmail()); // This is null if the 'email' scope is not present.
}
```

## 사용자 로그아웃

로그아웃 버튼이나 링크를 추가하여 사용자가 앱상에서 로그아웃하도록 할 수 있다.

로그아웃 링크를 만들려면 `GoogleAuth.signOut()` 메서드를 호출하는 함수를 링크의 `onclick` 이벤트에 연결하면 된다.

```html
<a href="#" onclick="signOut();">Sign out</a>
<script>
  function signOut() {
    var auth2 = gapi.auth2.getAuthInstance();
    auth2.signOut().then(function () {
      console.log("User signed out.");
    });
  }
</script>
```

## 참고사이트

[웹 앱에 Google 로그인 통합](https://developers.google.com/identity/sign-in/web/sign-in)<br/>
[사용자 정의 그래픽으로 버튼 만들기](https://developers.google.com/identity/sign-in/web/build-button#building_a_button_with_a_custom_graphic)
