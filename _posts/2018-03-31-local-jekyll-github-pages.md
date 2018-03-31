---
layout: post
title: 로컬에서 Jekyll 블로그 실행하기
category: 기타
excerpt_separator:  <!--more-->
---
변경 내용을 로컬에서 실행하고 테스트해보려면 몇 가지 준비가 필요하다.
[깃허브에서 제공하는 가이드](https://help.github.com/articles/setting-up-your-github-pages-site-locally-with-jekyll/)를 보고 따라했는데, 아무래도 윈도우와 한글이라는 특수함때문에 조금 어려움이 있었기에, 내가 했던 방법을 정리해본다.<br>

## Ruby와 Bundler 설치
Ruby는 [공식 홈페이지](https://www.ruby-lang.org/)에서 윈도우 인스톨러를 다운로드받아 설치할 수 있다. 이 때, Devkit이 포함된 버전을 설치해야 한다.
설치 마지막 단계에서 "Run 'ridk install' to ..." 가 체크되어 있는데, 그대로 진행한다. 아래와 같이 콘솔 창이 실행되면서 MSYS2를 설치할 수 있는 옵션을 제공한다.<br>
![RubyInstaller2](../_screenshots/RubyInstaller2.png?raw=true)<br>
모두 설치할 필요가 있는지는 잘 모르겠지만, 나는 1, 2, 3을 순서대로 설치하였다.<br>
MSYS2설치가 완료되면, 아래 명령어를 이용해 Bundler를 설치한다.
```
$ gem install bundler
```

## Jekyll 설치
블로그 소스코드 리포지토리에 다음과 같이 Gemfile을 생성한다. Gemfile이 이미 존재한다면, 내용이 맞는지 확인한다.
```bash
$ vi Gemfile
source 'https://rubygems.org'
gem 'github-pages', group: :jekyll_plugins
```

Jekyll과 의존성 라이브러리들을 설치한다.
```
$ bundle install
```

## 빌드

Jekyll을 실행한다.
```
$ bundle exec jekyll serve
```
그런데 아래와 같이 에러가 발생하였다.<br>
![error](/_screenshots/error.png?raw=true) <br>
검색해보니 인코딩 문제인 것 같아서 이것 저것 해보았는데, 여전히 같은 에러가 발생했다. 그러다 [같은 문제를 겪었던 분의 글](https://jprogram.github.io/articles/2017-12/Windows)을 찾을 수 있었다.
나는 모든 명령어를 Git-bash에서 실행하고 있었는데, Ruby 콘솔 창(Start Command Prompt with Ruby)에서 인코딩을 변경해야 했다.
```
> chcp 65001
> bundle exec jekyll serve
```
