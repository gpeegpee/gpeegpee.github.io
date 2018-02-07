---
layout: post
title: Jekyll 블로그에 AMP 적용하기
date: 2018-02-05
comments: true
tag:
  - AMP
  - Jekyll
  - Github
---

## AMP는 뭔가요?

AMP(Accelerated Mobile Pages)는 모바일 웹 로딩시간을 줄이기 제안된 오픈소스 프로젝트입니다. AMP의 작동 원리는 대략 3단계로 나뉘며, 핵심은 '캐싱'(Caching)입니다.

-   페이지 구성 단순화 : 자바스크립트 코드를 최소화합니다. 필요한 기능은 태그 컴포넌트로 만들어둡니다. 구글은 'AMP 자바스크립트'라는 라이브러리를 제공합니다.
-   대역폭 최적화 : 최적화된 해상도 이미지를 찾아 기기에 최적화된 콘텐츠 노출하고, 비동기 로딩을 통해 뉴스 소비 경험을 개선합니다. 비동기 로딩이란, 뉴스를 읽는 데 핵심이 되는 텍스트를 먼저 띄우고 용량이 큰 이미지를 나중에 받는 방식입니다.
-   페이지 캐싱 : 구글은 AMP를 적용한 뉴스 데이터를 저장(캐싱)합니다. 사용자가 뉴스를 읽겠다고 요청하면, 언론사의 서버가 아니라 미리 캐싱한 데이터를 보여줌으로써 로딩 시간을 획기적으로 줄입니다.

## Jekyll 블로그에 AMP를 어떻게 적용하나요?

-   Jekyll 블로그에 [AMP](https://ampbyexample.com/)를 적용하려면 몇가지 수정을 해야 합니다. 다음은 해당 블로그에서 사용하고 있는 [lanyon-plus jekyll theme](https://github.com/dyndna/lanyon-plus)를 기준으로 적용하면서 수정한 항목입니다.

### [수정한 내용]

-   amp 적용을 위해 [amp-jekyll](https://github.com/juusaw/amp-jekyll/tree/master/lib/jekyll)에서 ruby파일 2개를 다운받아 블로그 \_plugins폴더에 복사합니다.

-   \_config.xml에 아래 아래와 같이 필요한 package를 추가합니다.

```code
plugins:
  - fastimage
  - amp-jekyll
```

-   Gemfile에도 필요한 package를 추가합니다.

```code
gem 'fastimage'
gem 'amp-jekyll'
```

-   `<head></head>` 안에 amp-boilerplate를 추가합니다. lanyon-plus 기준으로는 \_include 폴더에 있는 head.html, head_minimal.html를 수정합니다.

```code
<style amp-boilerplate>body{-webkit-animation:-amp-start 8s steps(1,end) 0s 1 normal both;-moz-animation:-amp-start 8s steps(1,end) 0s 1 normal both;-ms-animation:-amp-start 8s steps(1,end) 0s 1 normal both;animation:-amp-start 8s steps(1,end) 0s 1 normal both}@-webkit-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-moz-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-ms-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-o-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}</style><noscript><style amp-boilerplate>body{-webkit-animation:none;-moz-animation:none;-ms-animation:none;animation:none}</style></noscript>
```

-   `<head></head>` 안에 amp async script를 추가합니다.

```code
<script async src="https://cdn.ampproject.org/v0.js"></script>
<script async custom-element="amp-analytics" src="https://cdn.ampproject.org/v0/amp-analytics-0.1.js"></script>
<script async custom-element="amp-iframe" src="https://cdn.ampproject.org/v0/amp-iframe-0.1.js"></script>
```

-   \_include 폴더에 있는 head.html, head_minimal.html내에 iconmoon.css와 style.min.css해당 하는 부분을 삭제하고 아래와 같이 amp-custom style로 만들어 줍니다.

{% raw %}

```code
<style amp-custom>
  {% include_absolute /public/css/iconmoon.css %}
  {% include_absolute /public/css/style.min.css %}
</style>
```

{% endraw %}

-   Jekyll에서는 기본적으로 \_include 밖에 있는 파일을 include할 수 없어 include_absolute plugin을 설치해야 합니다. [include_absolute_plugin](https://github.com/tnhu/jekyll-include-absolute-plugin/blob/master/include_absolute.rb)에서 ruby파일을 다운받아 블로그 \_plugins 폳더 밑에 복사합니다.

-   amp에서는 img tag 대신 amp-img를 사용합니다. 아래와 같이 amp-img로 수정합니다.

{% raw %}

```code
<amp-img width="150" height="150" src="https://chart.googleapis.com/chart?chs=150x150&cht=qr&chl={{ site.url }}{{ page.url }}&choe=UTF-8" alt="{{ site.url }}{{ page.url }}">
<noscript>
<img src="https://chart.googleapis.com/chart?chs=150x150&cht=qr&chl={{ site.url }}{{ page.url }}&choe=UTF-8" width="150" height="150" alt="{{ site.url }}{{ page.url }}"/>
</noscript>
</amp-img>
```

{% endraw %}

-   \_include폴더에 있는 scripts.html에서 google analytic script부분을 삭제하고 아래와 같이 수정합니다.

{% raw %}

```code
<amp-analytics type="googleanalytics">
<script type="application/json">
{
  "vars": {
    "account": "{{ site.google_analytics }}"
  },
  "triggers": {
    "trackPageview": {
      "on": "visible",
      "request": "pageview"
    }
  }
}
</script>
</amp-analytics>
```

{% endraw %}

-   필요한 meta tag를 추가합니다.

    -   `<head></head>` 안에 `<meta charset="utf-8">`를 추가합니다.
    -   `<head></head>` 안에 `<meta name="viewport" content="width=device-width,minimum-scale=1,initial-scale=1">`를 추가합니다. 기존 viewport를 정의한 부분이 있으면 삭제하고 추가합니다.

-   `<html>` tag에 `<html amp lang="en-us">`를 추가합니다.

-   Sidebar toggle script (해결중)
-   Disqus comment (해결중)

## amp가 적용되었는지는 어떻게 확인하나요?

-   amp가 적용되었는지 확인하기 위해서는 해당 URL뒤에 #development=1을 추가하여 페이지 로딩한 뒤 chrome inspect 메뉴에서 console tab에서 amp validation이 정상적으로 되었는지 로그를 통해 확인할 수 있습니다. 오류가 있는 경우에는 오류 내용과 함께 관련 링크를 제공합니다. 정상적인 경우에는 아래와 같이 성공메시지가 보입니다.

```code
Powered by AMP ⚡ HTML – Version 1516850240342
AMP validation successful.
```

## 참고

-   <http://www.bloter.net/archives/255539>
-   <http://www.bloter.net/archives/250056>
-   <https://lovefields.github.io/all/2017/01/31/post16.html>
-   <https://hanheesong.github.io/develope/amp-install/>
-   <https://joshua1988.github.io/web-development/amp/amp-getting-started/>
