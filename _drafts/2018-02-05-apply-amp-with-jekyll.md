---
layout: post
title: Jekyll 기반 블로그에 AMP 적용하기
date: 2018-02-05T00:00:00.000Z
comments: true
tag:
  - AMP
  - Jekyll
---

# AMP 개요

구글 AMP(Accelerated Mobile Pages)는 모바일 웹 로딩시간을 줄이기 위해 구글이 제안한 프로젝트입니다. AMP의 작동 원리는 대략 3단계로 나뉘며, 핵심은 '캐싱'(Caching)입니다.

- 페이지 구성 단순화 : 자바스크립트 코드를 최소화한다. 필요한 기능은 태그 컴포넌트로 만들어둔다. 구글은 'AMP 자바스크립트'라는 라이브러리를 제공한다.
- 대역폭 최적화 : 최적화된 해상도 이미지를 찾아 기기에 최적화된 콘텐츠 노출하고, 비동기 로딩을 통해 뉴스 소비 경험을 개선한다. 비동기 로딩이란, 뉴스를 읽는 데 핵심이 되는 텍스트를 먼저 띄우고 용량이 큰 이미지를 나중에 받는 방식이다.
- 페이지 캐싱 : 구글은 AMP를 적용한 뉴스 데이터를 저장(캐싱)한다. 사용자가 뉴스를 읽겠다고 요청하면, 언론사의 서버가 아니라 미리 캐싱한 데이터를 보여줌으로써 로딩 시간을 획기적으로 줄인다

## 참고

- <http://www.bloter.net/archives/255539>
- <http://www.bloter.net/archives/250056>

# Jekyll 블로그에 AMP 적용

## 아래

- _config.xml에 아래 package 추가

```code
plugins:
  - fastimage
  - amp-jekyll
```

- Gemfile에 package 추가

```code
gem 'fastimage'
gem 'amp-jekyll'
```

- AMP 에러 수정

  - Head tag에 아래 amp-boilerplate 추가(e.g. head.html or head_minimal.html)

```code
<style amp-boilerplate>body{-webkit-animation:-amp-start 8s steps(1,end) 0s 1 normal both;-moz-animation:-amp-start 8s steps(1,end) 0s 1 normal both;-ms-animation:-amp-start 8s steps(1,end) 0s 1 normal both;animation:-amp-start 8s steps(1,end) 0s 1 normal both}@-webkit-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-moz-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-ms-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-o-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}</style><noscript><style amp-boilerplate>body{-webkit-animation:none;-moz-animation:none;-ms-animation:none;animation:none}</style></noscript>
```

- amp async script 추가
- style 하나로 합치기
- amp-img 적용
- include_absolute 적용
- sidebar toggle script 해결

- Google Analytics 적용

- HTML Head tag 부분 수정

- Disqus 수정

# 참고

- <https://lovefields.github.io/all/2017/01/31/post16.html>
- <https://hanheesong.github.io/develope/amp-install/>
- <https://joshua1988.github.io/web-development/amp/amp-getting-started/>
