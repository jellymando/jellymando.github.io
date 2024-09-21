---
title: 'npm vs yarn ? yarn install 버전 에러 해결'
categories: [기타]
tags: [npm, yarn]
---

{:toc .large-only}

## npm & yarn

npm과 yarn은 대표적인 Node.js 패키지 관리 툴이다.

## package.json이란?

- 프로젝트 정보와 의존성(dependencies)을 관리하는 문서
- 패키지, 버전 등을 기록하여 다른 PC에서도 동일한 개발 환경을 구축

## npm vs yarn

|                     | npm                                                                          | yarn                                                              |
| :------------------ | :--------------------------------------------------------------------------- | ----------------------------------------------------------------- |
| 패키지 설치         | 순차 설치<br/>(패키지가 완전히 설치 될 때까지 기다린 후 다른 패키지를 설치)  | 병렬 설치                                                         |
| 속도                | yarn에 비해 느림                                                             | npm에 비해 빠름                                                   |
| 자동 lock 파일 생성 | package-lock.json 파일 자동 추가                                             | yarn.lock 파일 자동 추가                                          |
| 보안                | 다른 package를 즉시 포함 시킬 수 있는 코드를 자동으로 실행하므로 보안에 취약 | yarn.lock 또는 package.json에 있는 파일만 설치하므로 npm보다 안전 |

## 노트

사실 이 포스트는 `npm install`은 잘 실행되지만 `yarn install`은 에러가 나서 찾아본 내용이다.

node 버전이 맞음에도 맞지 않는다는 에러가 발생했다.

에러를 발생시키는 해당 모듈은 `package.json`에 있지도 않은데, `package-lock.json` 파일을 삭제해도 계속 에러가 났다.

구글링해보니 패키지 버전과 노드 엔진 간의 비호환성 때문에 발생하는 오류라고 한다.

아래 명령어를 터미널로 실행시키니 정상적으로 인스톨되었다.

```bash
yarn config set ignore-engines true
```

## 참고사이트

[[#.NPM] NPM vs YARN의 차이점을 알아보자](https://developer0809.tistory.com/128)<br/>
[[개발상식] npm과 yarn](https://velog.io/@kysung95/%EA%B0%9C%EB%B0%9C%EC%83%81%EC%8B%9D-npm%EA%B3%BC-yarn)<br/>
[The engine "node" is incompatible with this module](https://stackoverflow.com/questions/56617209/the-engine-node-is-incompatible-with-this-module)<br/>
[yarn에서 package.json 의 engines 설정 무시하기](https://velog.io/@bang9dev/yarn%EC%97%90%EC%84%9C-package.json-%EC%9D%98-engines-%EC%84%A4%EC%A0%95-%EB%AC%B4%EC%8B%9C%ED%95%98%EA%B8%B0)
