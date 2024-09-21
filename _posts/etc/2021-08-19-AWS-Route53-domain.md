---
title: "[AWS] Route 53에 도메인 등록하여 사용하기"
categories: [..etc]
tags: [aws]
---

{:toc .large-only}

### 도메인 등록하기

- [freenom.com](https://www.freenom.com/en/index.html)에서 무료 도메인을 만든다.

- `.tk, .ml, .ga, .cf, .gq` 다섯가지 최상위 도메인이 무료로 제공된다.

- 원하는 `도메인이름 + 최상위 도메인` 합쳐서 검색한 후 신청한다.

- 최대 12개월 무료이며 12개월이 되기 전에 renew를 해주면 계속 사용 가능하다고 한다.

### 호스팅 생성

- [AWS Route 53 호스팅 영역 생성 페이지](https://console.aws.amazon.com/route53/v2/hostedzones#CreateHostedZone)에 들어가서 로그인한다.

- 도메인 이름에 위에서 만든 도메인을 입력한 뒤 생성 버튼 클릭 (다른 항목은 미입력했음)

### 네임서버 등록

- 위에서 생성한 레코드를 클릭하면 NS 유형에 4개의 네임서버가 나온다.

<img src="/assets/img/blog/2021-08-19-AWS-Route53-domain_01.png">

- [freenom.com 사이트의 My Domains 페이지](https://my.freenom.com/clientarea.php?action=domains)로 들어간다.

- 도메인 우측의 [Manage Domain] 버튼을 클릭한다.

- Management Tools -> Nameservers 클릭

<img src="/assets/img/blog/2021-08-19-AWS-Route53-domain_02.png">

- 네임서버 4개를 입력한 후 저장한다.

<img src="/assets/img/blog/2021-08-19-AWS-Route53-domain_03.png">

### 레코드 생성

- 다시 AWS 호스팅 페이지로 돌아와서 레코드 생성 버튼을 클릭한다.

- 값 항목에 AWS 인스턴스와 연결된 탄력적 IP 주소를 입력한다. 탄력적 IP가 없다면 [탄력적 IP 주소 할당 페이지](https://us-east-2.console.aws.amazon.com/ec2/v2/home?region=us-east-2#AllocateAddress:)에서 발급받는다.

> 탄력적 IP로 설정하는 이유는, 기본 public IP는 유동 IP이기 때문에 새로 연결할 때마다 바뀌기 때문에 고정 IP로 설정하기 위함이다.

<img src="/assets/img/blog/2021-08-19-AWS-Route53-domain_04.png">

- 레코드 이름을 입력하지 않은 레코드를 하나 생성하고, 레코드 이름에 `www`를 넣은 레코드도 추가로 생성한다.

### 앱 서버 port 변경

앱 서버를 80번 외의 포트로 돌려놓으면 등록한 도메인에 포트번호를 붙여야 접속이 가능하다.

도메인 주소로 바로 접속해서 볼 수 있도록 앱 서버 포트를 리다이렉트 해준다.

SSH 서버 터미널에 접속해 앱 경로에서 아래 명령어를 입력한다.

```bash
sudo iptables -A PREROUTING -t nat -i eth0 -p tcp --dport 80 -j REDIRECT --to-port <앱 포트>
```

<br/>

그리고 중요한 것은 **우분투 서버에서는 로컬 아이피로 앱을 실행**해야 한다는 것이다.

로컬 IP로 앱을 실행하면, 탄력적 IP로 앱 서버에 접근 가능하다.

재부팅 시에는 포트 리다이렉트 작업을 다시 해줘야 하는 것 같다.

- 이제 모든 구축이 끝났다. 실제 도메인 및 라우팅이 되려면 대략 하루에서 하루 반나절 걸리는 것 같다. Good job~👍

### 참고사이트

[AWS EC2에 무료 도메인 등록하기](https://dawitblog.tistory.com/92)<br/>
[[AWS] Route 53 : DNS서비스 이용하기](https://happiestmemories.tistory.com/47)<br/>
[AWS Route 53 에 도메인 등록하여 사용하기](https://medium.com/@labcloud/aws-route-53-%EC%97%90-%EB%8F%84%EB%A9%94%EC%9D%B8-%EB%93%B1%EB%A1%9D%ED%95%98%EC%97%AC-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0-e2d9da2e864d)
