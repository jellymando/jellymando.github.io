---
layout: post
title: "[ubuntu] GUI, 원격 데스크톱(Xrdp) 설치하기"
sitemap: false
---

{:toc .large-only}

우분투 서버에 파일을 만들고 수정해야 해서 원격 접속이 필요했다.

원격 접속을 위해서는 우분투에 GUI와 원격 데스크톱을 설치해야 한다.

### SSH 접속

[[AWS의 기본 04] EC2 인스턴스에 SSH로 접속하기](https://wingsnote.com/53)

### GUI 설치

- 우선 사용자 패스워드를 설정한다.

```bash
sudo passwd ubuntu
```

- apt-get 도구 업데이트, 업그레이드

```bash
sudo apt-get update
sudo apt-get upgrade
```

- ubuntu-desktop 설치

```bash
sudo apt-get install --no-install-recommends ubuntu-desktop
```

위는 최소 설치이고 전체 설치(기본 프로그램 모두 설치)는 아래 코드를 입력한다.

```bash
sudo apt-get install ubuntu-desktop
```

- 실행

아래 코드를 원격 데스크톱까지 설치한 후 실행한다.

```bash
sudo startx
```

<br/>

[리눅스 우분투 gui 설치 ( ubuntu server 16.04 LTS )](https://wlsvud84.tistory.com/26)

### 원격 데스크톱(Xrdp) 설치

- xrdp와 xfce4 설치

```bash
sudo apt-get install xrdp
sudo apt-get install xfce4
```

- xfce4 가 기본 메니져가 되도록 설정

```bash
sudo echo xfce4-session>~/.xsession
```

- 서비스 리스타트

```bash
sudo service xrdp restart
```

- RDP(Remote Desktop Protocol) 연결 포트 확인

```bash
sudo vi /etc/xrdp/xrdp.ini
```

- AWS 인스턴스 인바운드 규칙에 위 port와 5910 포트 추가한다.

<img src="/assets/img/blog/2021-08-19-AWS-Route53-domain_04.png">

<br/>

[[AWS] 인바운드 규칙 설정하기](https://dbjh.tistory.com/65)

- mate-desktop 설치

```bash
sudo apt-get update sudo apt-get install mate-core mate-desktop-environment mate-notification-daemon
```

- GUI 실행

```bash
sudo startx
```

- 윈도우에서 원격 데스크톱 연결

AWS public ip, 사용자 이름은 ubuntu로 입력하고 설정했던 비밀번호로 연결

맥에서는 원격 연결 안해봤다. 혹시 몰라 서치했던 링크 아래에 첨부.

<br/>

[맥(Mac OS X)에서 원격 접속하기](https://davelogs.tistory.com/84)

### 참고사이트

[AWS EC2 Ubuntu RDP(원격데스크톱) 연결하기](https://all-share-source-code.tistory.com/18)<br/>
[우분투 16.04 VNC를 이용한 원격 데스크톱 설정 및 접속 방법](https://extrememanual.net/12210)<br/>
[원격 테스크탑으로 우분투 원격 접속하기](https://blog.daum.net/keydream/14636077)<br/>
[AWS – EC2 – UBUNTU – XRDP 환경 구성](https://hugrypiggykim.com/2016/07/10/aws-ec2-ubuntu-xrdp-%ED%99%98%EA%B2%BD-%EA%B5%AC%EC%84%B1/)<br/>
[우분투 16.04 원격 데스크탑 설정](https://goodtogreate.tistory.com/entry/%EC%9A%B0%EB%B6%84%ED%88%AC-1604-%EC%9B%90%EA%B2%A9-%EB%8D%B0%EC%8A%A4%ED%81%AC%ED%83%91-%EC%84%A4%EC%A0%95)<br/>
