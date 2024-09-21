---
title: "[Github 블로그 에러] Page build failure"
categories: [..etc]
tags: [github]
---

{:toc .large-only}

## 문제

github 블로그에 포스트를 push 했는데 몇 시간이 지나도 블로그가 업데이트 되지 않았다.

github 서버 문제인 줄 알고 기다렸지만 며칠 뒤 확인해도 포스트가 올라오지 않았다..;;

메일함을 보니 블로그에 push할 때마다 'Page build failure' 라는 메일이 와 있었다.

jekyll 관련 파일을 수정한 적도 없고, 그저 포스트만 올렸을 뿐인데..

[github Action](https://github.com/jellymando/jellymando.github.io/actions) 페이지에 들어가보니 build 단계에서 계속 에러가 나고 있었고..

로그를 보니 `/usr/local/bundle/gems/jekyll-3.9.0/lib/jekyll/theme.rb:84:in 'rescue in gemspec': The jekyll-theme-hydejack theme could not be found. (Jekyll::Errors::MissingDependencyException)` 라는, theme를 찾을 수 없다는 에러가 뜨고 있었다.

jekyll-theme-hydejack 테마를 사용하고 있었는데, 이 테마가 없어진 건가 싶어 해당 테마의 github에 들어가봤지만 여전히 건재했다.

그렇게 2시간 가량 구글링을 하다가 겨우 해결할 수 있었다.

## 해결

[hydejack Install](https://hydejack.com/docs/install/#github-pages) 페이지에서 GitHub Pages 설정하는 방법을 참고하여 `_config.yml` 파일을 수정했다.

기존에는 `remote_theme` 값이 `hydecorp/hydejack@v9.0.0` 이었는데 `remote_theme: hydecorp/hydejack@v9.1.5` 로 변경했다.

하지만 그래도 에러가 나서 [hydejack gh-pages branch](https://github.com/hydecorp/hydejack-starter-kit/tree/gh-pages)를 참고했다!

해당 브랜치의 `_config.yml` 파일을 보니 `theme: jekyll-theme-hydejack` 코드 앞에 주석이 되어 있었다..!

바로 내 블로그의 `_config.yml` 파일에서 해당 코드를 똑같이 주석처리하고 push 하니까 더 이상 `The jekyll-theme-hydejack theme could not be found.` 에러가 뜨지 않았고 드디어 블로그가 정상 업데이트 되었다. ㅎㅎ

```bash
# Theme
# ---------------------------------------------------------------------------------------

# theme: jekyll-theme-hydejack
remote_theme: hydecorp/hydejack@v9.1.5
```
