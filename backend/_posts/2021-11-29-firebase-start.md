---
layout: post
title: "[Firebase] 시작하기"
sitemap: false
---

{:toc .large-only}

## Firebase Project 시작하기

1. [Firebase console](https://console.firebase.google.com/)에서 **[프로젝트 추가]** 클릭
1. 프로젝트 정보 입력
1. 프로젝트 생성 완료

## Project에 앱 추가하기

1. 생성된 프로젝트 클릭
1. **"앱에 Firebase를 추가하여 시작하기"** 문구 밑의 앱 아이콘 클릭
1. 앱 이름 입력
1. **[콘솔로 이동]** 클릭

## Cloud Firestore 추가하기

1. 좌측 메뉴의 **[Firestore database]** 클릭
1. **[데이터베이스 만들기]** 클릭
1. **[테스트 모드에서 시작]** 선택 (local에서 데이터 요청 시)
1. Cloud Firestore 위치 설정 (서울: **asia-northeast3**)
1. 데이터베이스 생성 완료

## Firestore에 Collection 추가하기

1. **[컬렉션 시작]** 클릭
1. 컬렉션 ID 입력 (상위집합)
1. 문서 ID 입력 (하위집합)
1. 필드 이름/타입 입력

## React 앱에 연동

1. firebase 모듈 설치 `npm install firebase`
1. 리액트 앱에서 `firebase.js` 파일 생성
1. firebase의 프로젝트 설정 페이지 하단의 [내 앱] - [SDK 설정 및 구성] 항목의 SDK 코드 복사
1. 3에서 복사한 코드를 2의 파일에 붙여넣기

## 참고사이트

[ReactJS | Firebase로 React 프로젝트 DB 연동 및 배포](https://pathas.tistory.com/214)<br/>
[[Firebase] Cloud Firestore 데이터 생성 방법](https://copycoding.tistory.com/314)
