---
title: "[JSP] 표현 언어"
categories: [JSP]
tags: [jsp]
---

{:toc .large-only}

## 표현 언어

- JSP 2.0 버전부터 추가된 간결한 수식 언어
- EL(Expression Language)이라고도 함
- 스크립트 요소 밖에서 사용
- 표현식 `<%= %>`을 대신함
- 데이터를 출력하거나 태그의 속성 값을 지정할 때 사용
  - 수식, 관계, 논리 연산자 제공
  - 자바 클래스 메서드를 이용한 함수 호출 기능 제공
  - JSP 내장 객체의 속성과 자바빈 객체를 사용할 수 있음
  - 별도의 내장 객체 제공

### 기본 형식

- `${수식}`
  - `${객체}`
  - `${객체.속성}`
  - `${객체["속성"]}`
  - `${객체['속성']}`
  - `${객체[첨자]}`

```cpp
<jsp:include page="/${image.file}/view_image.jsp" flush="true" />
<b>${sessionScope.member.name}</b>님 어서오세요.
${(6 > 3) ? 7 : 8}
```

### 표현 언어의 내장 객체

| 내장 객체        | 설명                                                                                                                                    |
| ---------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| pageScope        | pageContext 내장 객체에 저장된 속성의 <이름, 값>을 저장한 Map 객체                                                                      |
| requestScope     | request 내장 객체에 저장된 속성의 <이름, 값>을 저장한 Map 객체                                                                          |
| sessionScope     | session 내장 객체에 저장된 속성의 <이름, 값>을 저장한 Map 객체                                                                          |
| applicationScope | application 내장 객체에 저장된 속성의 <이름, 값>을 저장한 Map 객체                                                                      |
| param            | request.getParameter() 함수의 결과와 동일한 Map 객체                                                                                    |
| paramValues      | request.getParameterValues() 함수의 결과와 동일한 Map 객체                                                                              |
| header           | request.getHeader() 함수의 결과와 동일한 Map 객체                                                                                       |
| headerValues     | request.getHeaders() 함수의 결과와 동일한 Map 객체                                                                                      |
| cookie           | request.getCookies() 함수의 결과인 Cookie 배열을 <쿠키이름, Cookie 객체> 형태로 저장한 Map 객체<br/>Cookie 객체는 <이름, 값>으로 구성됨 |
| initParam        | application.getInitParameter() 함수의 결과와 동일한 Map 객체                                                                            |
| pageContext      | JSP의 pageContext 내장 객체와 동일                                                                                                      |

```cpp
요청 URI: ${pageContext.request.requestURI}<br/>
request의 name 속성의 값: ${requestScope.name}<br/>
파라미터의 code 값: ${param.code}
쿠키의 name 값: ${cookie.name.value}
쿠키의 phone 값: ${cookie.phone.value}
```

#### 자바빈 객체 사용하기

```jsp
<%@page language="java" contentType="text/html; charset=UTF-8" %>
<jsp:useBean id="score1" class="com.school.Score" scope="page" />
<jsp:setProperty name="score1" property="name" value="Jimmy" />
<jsp:setProperty name="score1" property="kor" value="90"/>
<jsp:setProperty name="score1" property="eng" value="85"/>
<jsp:setProperty name="score1" property="math" value="95" />
<html>
이름 : ${score1.name}<br>
국어 : ${score1.kor}<br>
영어 : ${score1.eng}<br>
수학 : ${score1.math}
</html>
```
