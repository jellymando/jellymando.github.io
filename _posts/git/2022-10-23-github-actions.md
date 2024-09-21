---
title: "자동으로 github에 잔디 깔기"
categories: [GIT]
tags: [git, github actions, schedule]
---

{:toc .large-only}

(허접한) 자동 커밋 프로그램 만들어보기

## python 파일 생성

우선 README 파일을 업데이트 해주는 python 파일을 만들어준다.

시간대는 pytz 라이브러리를 사용하여 서울 시간 기준으로 맞춰줬다.

```py
from datetime import datetime
import pytz

readme = open("README.md", "w")
time = datetime.now(pytz.timezone('Asia/Seoul'))
readme.write("last update time : " + str(time) + "\n")
print(str(time))
readme.close()
```

## 시작은 GitHub Actions 였지만..

GitHub의 Actions 기능을 활용하면 CI/CD를 설정할 수 있다.

1. 자동 배포를 설정할 브랜치를 만들고 Actions 메뉴로 들어간다.

<img src="/assets/img/blog/2022-10-23-github-actions_01.png">

1. New workflow 버튼을 클릭한다.

<img src="/assets/img/blog/2022-10-23-github-actions_02.png">

1. Python application을 검색하여 선택한다.

## xml 작성

위에서 만든 python 파일을 실행시키고 커밋해주는 xml 파일을 작성한다.

```xml
# This workflow runs update_readme.py which updates README.md file.

name: Update readme # GitHub Actions 탭에서 확인할 수 있는 액션 이름

on: # jobs가 실행되어야 하는 상황 정의
  push:
    branches: ["main"] # main 브랜치에 push가 발생했을 때
  # pull_request:
  #   branches: ["main"] # main 브랜치에 pull request가 발생했을 때
  schedule:
    - cron: "*/5 * * * *" # 5분마다 실행

jobs: # 실제 실행될 내용
  update_readme:
    runs-on: ubuntu-latest # 빌드 환경
    steps:
      - uses: actions/checkout@v3 # checkout
      - name: Set up Python 3.10
        uses: actions/setup-python@v3 # setup-python
        with:
          python-version: "3.10" # 3.10버전 파이썬 사용
      - name: Install dependencies # 1) 스크립트에 필요한 dependency 설치
        run: |
          python -m pip install --upgrade pip
          pip install python-leetcode
      - name: Run update_readme.py # 2) update_readme.py 실행
        run: |
          python update_readme.py
      - name: Commit changes # 3) 추가된 파일 commit
        run: |
          git pull
          git config --global user.email 'cicikdi@naver.com'
          git config --global user.name 'jellymando'
          git add .
          git commit -m "Auto update README.md"
          git push
```

`on`에서 `push: branches:`를 설정하면 해당 브랜치에 푸시할 때마다 jobs를 실행한다.

이것은 잘 동작한다. 하지만..

`schedule`에 `- cron` 값을 설정하면 해당 시간마다 jobs를 실행한다.

cron에 설정한 시간대로 jobs가 실행되지 않았다.

firebase의 Cloud Functions을 이용해서 자동 실행 프로그램을 돌릴 수도 있지만 유료라고 한다.

## bat 파일 생성

서버를 이용할 수 없다면 간단한 bat 파일을 만들어서 컴퓨터를 부팅할 때마다 실행해서 알아서 커밋하도록 만들겠다는 단순한 방법을 떠올렸다.

자동 배포할 브랜치에 위에서 만든 xml 내용 일부를 복붙하여 bat 파일을 생성했다.

```bat
python update_readme.py
git pull
git config --global user.email 'cicikdi@naver.com'
git config --global user.name 'jellymando'
git add .
git commit -m "Auto update README.md"
git push
```

윈도우+R 키를 누르고 shell:startup를 실행한 후 위에서 만든 bat 파일 바로가기를 생성하여 붙여넣어준다.

이제 컴퓨터를 켤 때마다 자동으로 깃에 커밋된다. ㅎ

## 윈도우 자동 스케줄러 설정

부팅을 매일 하는게 아니기 때문에 윈도우 내에서 매일 bat을 실행시키도록 스케줄러도 추가하였다.

1. 윈도우에 작업 스케줄러 검색

1. 기본 작업 만들기 클릭

1. 이름 설정

1. 작업 시간 설정

<img src="/assets/img/blog/2022-10-23-github-actions_03.png">

1. bat 파일 지정

1. 조건, 설정 설정

<img src="/assets/img/blog/2022-10-23-github-actions_04.png" style="margin-bottom: 25px;">

"컴퓨터의 AC 전원이 켜져있는 경우에만.." 체크 해제

<img src="/assets/img/blog/2022-10-23-github-actions_04.png" style="margin: 0 25px;">

"작업이 실패하는 경우 다시 시작.." 체크

## 참고사이트

[[Git] github actions로 README.md 자동생성하기](https://holika.tistory.com/entry/Git-github-actions%EB%A1%9C-READMEmd-%EC%9E%90%EB%8F%99%EC%83%9D%EC%84%B1%ED%95%98%EA%B8%B0)<br/>
[github actions로 자동 1일 1커밋 봇 만들기](https://this-programmer.tistory.com/490)<br/>
[GitHub Actions 워크플로우 사용하기](https://blog.outsider.ne.kr/1510)<br/>
[schedule](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows#schedule)
