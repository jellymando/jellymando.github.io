---
title: 'UNIX 쉘 스크립트 npm 패키지 버전 비교문 작성하기'
categories: [..etc]
tags: [unix]
---

{:toc .large-only}

npm 패키지 버전을 체크하여 버전이 다른 경우에만 publish하는 쉘 스크립트 코드를 작성하였다. (ChatGPT 참고)

```shell
# 현재 패키지 버전
current_version=$(node -pe "require('./package.json').version")

# 마지막으로 업데이트한 패키지 버전
latest_version=$(npm view <package-name> version || echo "0.0.0")

# 버전 비교 및 분기
if [[ "$current_version" == "$latest_version" ]]; then
  echo "Package is already up to date. Skipping publishing."
else
  echo "Publishing package..."
  # Run your publish command here
  npm publish
fi
```

- if문을 사용하고 스크립트를 끝마치기 위해 `fi` 키워드를 넣어야한다.
- `[[ "$current_version" == "$latest_version" ]]:`
  - 이중 괄호 `[[...]]`를 사용한 조건식으로, Bash에서 지원하는 고급 형태의 조건식
  - 패턴 일치 및 정규 표현식과 같은 추가 기능을 허용
- `latest_version=$(npm view <package-name> version || echo "0.0.0")`
  - 아직 npm에 퍼블리싱 되지 않아서 `npm view <package-name> version`에서 실패하는 경우 스크립트가 종료되는 것을 방지하기 위해 `|| echo "0.0.0"`으로 기본 버전을 추가했다.
