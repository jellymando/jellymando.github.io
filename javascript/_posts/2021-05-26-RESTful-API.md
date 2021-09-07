---
layout: post
title: "RESTful API란? ✨"
sitemap: false
---

{:toc .large-only}

## REST

**Re**presentational **S**tate **T**ransfer의 약자로,

- 대표적인 상태 전달
- 네트워크 상에서 Client와 Server 사이의 통신 방식
- URI(<u>Uniform Resource Identifier</u>)를 통해 웹의 자원(<u>Resource</u>)을 명시
- HTTP Method(POST, GET, PUT, DELETE)를 통해 Resource에 대한 CRUD를 처리하도록 설계된 아키텍쳐

> CRUD: 컴퓨터 소프트웨어가 가지는 기본적인 데이터 처리 기능. **C**reate, **R**ead, **U**pdate, **D**elete

## REST 구성 요소

### 1. 자원(Resource): URI

- 모든 자원에 고유한 ID가 존재하고, 이 자원은 Server에 존재한다.
- 자원을 구별하는 ID는 ‘/groups/:group_id’와 같은 HTTP URI 다.
- Client는 URI를 이용해서 자원을 지정하고 해당 자원의 상태(정보)에 대한 조작을 Server에 요청한다.

### 2. 행위(Verb): HTTP Method

- HTTP 프로토콜의 Method(GET, POST, PUT, DELETE)를 사용한다.

### 3. 표현(REST)

- Client가 자원의 상태(정보)에 대한 조작을 요청하면 Server는 이에 적절한 응답(Representation)을 보낸다.
- REST에서 하나의 자원은 JSON, XML, TEXT, RSS 등 여러 형태의 Representation으로 나타내어 질 수 있다.
- JSON 혹은 XML를 통해 데이터를 주고 받는 것이 일반적이다.

<img src="/assets/img/blog/RESTful_API_01.png">

## REST 특징

### 1. Server-Client(서버-클라이언트 구조)

- 자원을 요청하는 쪽이 Client, 자원이 있는 쪽이 Server가 된다.
- REST Server: API를 제공하고 비즈니스 로직 처리 및 저장을 책임진다.
- Client: 사용자 인증이나 context(세션, 로그인 정보) 등을 직접 관리하고 책임진다.
- 서로 간 의존성이 줄어든다.

### 2. Stateless(무상태)

- HTTP 프로토콜은 Stateless Protocol이므로 REST 역시 무상태성을 갖는다.
- Client의 context를 Server에 저장하지 않는다.
  - 즉, 세션과 쿠키와 같은 context 정보를 신경쓰지 않아도 되므로 구현이 단순해진다.
- Server는 각각의 요청을 완전히 별개의 것으로 인식하고 처리한다.
  - 각 API 서버는 Client의 요청만을 단순 처리한다.
  - 즉, 이전 요청이 다음 요청의 처리에 연관되어서는 안된다.
  - 물론 이전 요청이 DB를 수정하여 DB에 의해 바뀌는 것은 허용한다.
  - Server의 처리 방식에 일관성을 부여하고 부담이 줄어들며, 서비스의 자유도가 높아진다.

### 3. Cacheable(캐시 처리 가능)

- 웹 표준 HTTP 프로토콜을 그대로 사용하므로 캐싱 기능을 적용할 수 있다.
  - HTTP 프로토콜 표준에서 사용하는 Last-Modified 태그나 E-Tag를 이용하면 캐싱 구현이 가능하다.
- 대량의 요청을 효율적으로 처리하기 위해 캐시가 요구된다.
- 캐시 사용을 통해 응답시간이 빨라지고 REST Server 트랜잭션이 발생하지 않기 때문에 전체 응답시간, 성능, 서버의 자원 이용률을 향상시킬 수 있다.

### 4. Layered System(계층화)

- Client는 REST API Server만 호출한다.
- REST Server는 다중 계층으로 구성될 수 있다.
- PROXY, 게이트웨이 같은 네트워크 기반의 중간 매체를 사용할 수 있다.

### 5. Code-On-Demand(optional)

- Server로부터 스크립트를 받아서 Client에서 실행한다.
- 반드시 충족할 필요는 없다.

### 6. Uniform Interface(인터페이스 일관성)

- URI로 지정한 Resource에 대한 조작을 통일되고 한정적인 인터페이스로 수행한다.
- **HTTP 표준 프로토콜에 따르는 모든 플랫폼에서 사용이 가능**하다.
- 특정 언어나 기술에 종속되지 않는다.

## RESTful API

- REST 기반으로 API를 제공하는 웹 서비스를 RESTful 하다고 할 수 있다.

- API의 엔드포인트 구조를 구현하는 방식

- API에서 전송하는 자원(resource)을 URI로 표현하고 해당 자원에 행하고자 하는 의도를 HTTP 메소드로 정의

- 각 엔드포인트는 리소스를 표현하는 고유의 URI(Uniform Resource Identifier) 주소를 가지고 있으며, 해당 리소스에 행할 수 있는 행위를 표현하는 HTTP 메소드를 처리할 수 있게 된다.

<img src="/assets/img/blog/RESTful_API_02.png"><br/>

<img src="/assets/img/blog/RESTful_API_03.png">

> API(Application Programming Interface) : 데이터와 기능의 집합을 제공하여 컴퓨터 프로그램간 상호작용을 촉진하며, 서로 정보를 교환가능 하도록 하는 것

## RESTful의 목적

- 이해하기 쉽고 사용하기 쉬운 REST API를 만드는 것

## RESTful API 규칙

### 1. URI를 사용하여 어떤 리소스인지 표현하자.

예를 들어, 서비스를 사용하는 유저의 목록을 가져오는 API가 있다면 리소스는 유저가 될 것이고, 이 API의 URI는 명확하게 유저를 표현하고 있어야 한다.

```js
GET / users;
```

users라는 복수형으로 표현하는 이유는 유저라는 리소스가 특정한 하나의 객체가 아니기 때문이다.

특정 유저를 표현하기 위해서는 계층을 이용한다.

### 2. 리소스의 계층을 표현하기

유저가 각각 고유한 ID를 가지고 있다면 슬래시 구분자(/)를 사용하여 계층 구조를 아래와 같이 표현할 수 있다.

```js
GET / users / 2;
```

<img src="/assets/img/blog/RESTful_API_04.png">

가령 위와 같은 계층 구조는 아래와 같이 표현할 수 있다.

```js
/users/2/profile-image
// 유저들 중 2번 유저의 프로필 사진
```

REST API는 분명한 URI를 만들어 통신을 해야 하기 때문에 혼동을 주지 않도록 URI 경로의 마지막에는 슬래시(/)를 사용하지 않는다.

### 3. URI에는 행위가 표현되면 안된다.

RESTful API는 URI를 사용하여 행위를 표현하지 않을 것을 권고한다.

URI가 가지는 의미는 철저히 어떤 리소스인지, 그리고 리소스의 계층 구조에 대한 것 뿐이어야 한다.

```js
POST /users/2/delete
```

### 4. HTTP 메소드를 사용하여 어떤 행위인지 표현하자.

<br/>

| Method |           의미            |
| ------ | :-----------------------: |
| GET    |    리소스를 조회한다.     |
| POST   |    리소스를 생성한다.     |
| DELETE |    리소스를 삭제한다.     |
| PUT    |    리소스를 대체한다.     |
| PATCH  | 리소스의 일부를 수정한다. |

<br/>

> **PUT과 PATCH의 차이**<br/> <img src="/assets/img/blog/RESTful_API_05.png"><br/>
> PUT은 유저 리소스를 대체하는 것이기 때문에 name을 ethan으로 수정할 때 리소스 전체를 보내야 한다.<br/>  
> <img src="/assets/img/blog/RESTful_API_06.png"><br/>
> PATCH는 유저 리소스를 수정하는 것이기 때문에 수정하고 싶은 사항만 보내면 된다.

### 5. 밑줄(\_) 대신 하이픈(-)을 사용하자.

가독성을 위해 밑줄보다 하이픈을 사용하자.

### 6. 대문자보다 소문자를 사용하자.

URI 경로에 대문자 사용은 피하도록 한다.

> RESTful 하지 못한 경우<br/>
> ex) CRUD 기능을 모두 POST로만 처리하는 API<br/>
> ex) endpoint에 resource, id 외의 정보가 들어가는 경우 (students/updateName)

## 참고사이트

[[Session] RESTful API 란? / Path parameters / Query string
](https://velog.io/@haileeyu21/Session-RESTful-API-%EB%9E%80-Path-parameters-Query-string)<br/>
[[Network] REST란? REST API란? RESTful이란?](https://gmlwjd9405.github.io/2018/09/21/rest-and-restful.html)<br/>
[프론트엔드와 백엔드가 소통하는 엔드포인트, RESTful API](https://evan-moon.github.io/2020/04/07/about-restful-api/)
