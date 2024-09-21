---
title: "[Firebase] React 앱에 연동하기"
categories: [BACKEND]
tags: [firebase]
---

{:toc .large-only}

## firebase 설치

```bash
npm install firebase
```

## Firebase SDK 사용

1. 리액트 앱에서 `firebase.js` 파일 생성
1. [firebase](https://console.firebase.google.com/) 프로젝트 설정 페이지 하단의 [내 앱] - [SDK 설정 및 구성] 항목의 SDK 코드 복사
1. 2에서 복사한 코드를 1의 파일에 붙여넣기

> `apiKey` 등은 `.env.local` 파일로 관리한다.

```js
import { initializeApp } from "firebase/app";
import { getFirestore } from "firebase/firestore";

const firebaseConfig = {
  apiKey: // API_KEY,
  authDomain: // PROJECT_ID.firebaseapp.com,
  projectId: // PROJECT_ID,
  storageBucket: // PROJECT_ID.appspot.com,
  messagingSenderId: // MESSAGING_SENDER_ID,
  appId: // APP_ID,
  measurementId: // MEASUREMENT_ID,
};

const app = initializeApp(firebaseConfig);
const db = getFirestore(app);
export default db;
```

## 데이터 가져오기

`collection, getDocs` 메서드를 이용해 컬렉션의 문서 데이터를 가져올 수 있다.

```js
import { collection, getDocs } from "firebase/firestore";

const querySnapshot = await getDocs(collection(db, "users"));
querySnapshot.forEach((doc) => {
  console.log(`${doc.id} => ${doc.data()}`);
});
```

> Next.js 에서 `getStaticProps()`를 통해 데이터를 가져오는 경우 SerializableError가 발생해서 `getDocs()` 함수를 `JSON.stringify()`로 감싸줬다.

## 참고사이트

[Cloud Firestore 시작하기](https://firebase.google.com/docs/firestore/quickstart)
