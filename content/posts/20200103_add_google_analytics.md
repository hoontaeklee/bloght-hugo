---
title: "Hugo 블로그에 Google analytics 추가하기"
date: 2020-01-03T20:33:22+09:00
description:
draft: false
hideToc: false
enableToc: true
enableTocContent: false
tocPosition: outer
tocLevels: ["h2", "h3", "h4"]
tags:
- Hugo
- Customizing
- 2020
categories:
- Blog Maintenance
---

## 서론

블로그는 사막에서 혼자 지낸다는 마음가짐으로 하는 것이지만, 그래도 누가누가 내 블로그에 오는지는 알고 싶은 법이다. 이를 위해 Google Analytics (GA)를 설치한다. [이 글](http://cloudywithachanceofdevops.com/posts/2018/05/17/setting-up-google-analytics-on-hugo/)의 내용을 따라했다. 웹사이트에 GA를 추가하려면 두 가지가 필요하다:
- Google Analytics 계정
- Google Analytics를 추가할 Hugo 웹사이트

## Google Analytics 계정 및 추적 ID 생성

[여기](https://marketingplatform.google.com/about/analytics/)에서 Google Analytics 계정을 생성한다.

GA는 웹사이트나 어플리케이션 등에 대한 데이터를 수집해주는 도구이다. 웹사이트의 경우 수집하는 데이터 종류는 방문한 사람 수, 방문한 사람의 유형, 유입 경로, 취한 행동(회원가입, 다운로드 등)에 따른 방문자 유형 등이다.

GA는 **계정(account)** - **속성(property)** - **보기(view)** 로 구성된다. **속성** 이란 데이터를 수집하고자 하는 웹사이트, 어플리케이션을 의미한다. **계정** 을 생성하고 추적하고자 하는 속성을 추가해 관리하는 방식이다. 각 속성에서는 **보기** 를 이용해 각 속성에서 어떤 데이터를 수집할 것인지 정할 수 있고, 이와 관련된 요약 보고서를 생성 및 열람할 수 있다. GA에 대한 자세한 정보는 [여기](https://ga-study.tistory.com/4)에 잘 정리돼있다.

계정에 블로그 웹사이트를 속성으로 추가하고 자동으로 생성된 추적 ID(Tracking ID)를 확인한다. **UA-123456789-1** 형식으로 돼 있고, 비밀번호 같은 개념이므로 **공유하지 않도록 한다.**

## Hugo 웹사이트에 Google Analytics 추가

앞서 얻은 **추적 ID** 를 **config.toml (or config.yaml)** 의 `googleAnalytics` 변수에 추가하고 저장한다:

```
baseURL: https://examplesite.com
languageCode: en-us
defaultContentLanguage: en
title: author
theme: hugotheme
googleAnalytics: UA-123456789-1 <!-- 여기 -->
disqusShortname: author
enableGitInfo: true
```

## 작동 확인

원래는 1) 추적 Id를 설정하고, 2) Hugo의 GA internal template을 turn on해야 완성이다.    
**하지만** 어떤 테마는 추적 ID만 입력하면 자동으로 GA가 활성화되기도 한다. 자신이 쓰는 테마가 이런 경우에 속한다면 여기서 설치 완료하면 된다.  

작동 확인 방법은 직접 블로그 주소에 접속해보는 것이다(`https://<username>.gitub.io`).

---

**\*\*주의**  
작동 확인을 위해 `hugo server` 명령을 이용해 로컬 웹서버를 열어볼 수도 있겠지만, 자신이 사용한 테마가 로컬 서버는 접속자 모니터링 대상에서 제외했을 수도 있다.

내가 사용한 `cupper-hugo-theme`이 그런 경우다.

`/layouts/partials/google-analytics-async.html`을 보면,

```
{{ if not .Site.IsServer }}
  {{ with .Site.GoogleAnalytics }}
  <script>
  window.ga=window.ga||function(){(ga.q=ga.q||[]).push(arguments)};ga.l=+new Date;
  ga('create', '{{ . }}', 'auto');
  ga('send', 'pageview');
  </script>
  <script async src='https://www.google-analytics.com/analytics.js'></script>
  {{ end }}
{{ end }}
```

위와 같이 `{{ if not .Site.IsServer }}`과 `{{ end }}`로 묶여있는 것을 볼 수 있다. 이 코드가 `hugo server`로 접속한 로컬 서버를 제외하는 기능인 듯하다.

---

 그리고 GA의 모니터링 페이지를 확인한다. **만약 잘 작동하고 있다면** 현자 접속자 수가 1 이상일 것이고, **작동하고 있지 않다면** 현재 접속자 수가 0일 것이다.

GA에서 해당 속성 페이지의 실시간 개요 페이지를 연다(**크롬**, **웨일** 기준으로는 북마크 페이지 아래에 맨 왼쪽에 **GA로고** 가 있고, 다음으로 **"애널리틱스"** 글자가 나오고 그 오른쪽에 계정-속성을 선택할 수 있는 단추가 있다).

![](/posts/20200103_google_analytics_on_hugo/20200103_google_analytics_on_Hugo_fig1.jpg)

현재 활성 사용자 수가 1명으로 나온다. 이리저리 페이지를 옮겼기 때문에 우측 상단에 초당 페이지 뷰 수에 막대가 촘촘하게 생겼다. 그리고 사용 중 페이지도 잘 모니터링 되고 있다.  
반면, 로컬 서버로 접속하면 위와 같은 변화가 나타나지 않는다.



## Hugo Internal Template for Google Analytics 활성화

추적 ID 입력하는 것만으로 활성화가 되지 않는다면, 수동으로 GA 템플릿을 활성화 해야 한다.

이 글에서는 `header.html`에 GA를 추가한다. 이렇게 하면 블로그 내 모든 페이지에서 작동하게 된다(고 한다). 추가할 위치는 필요에 따라 다른 곳으로 선택해도 된다.

1. layouts/partials/header.html을 연다. (**head.html과 헷갈리지 말자**)

- 블로그 `root` 폴더 내 `layouts` 폴더에 `partials` 폴더를 만들어서 여기에 `header.html`을 생성하도록 한다. 직접 `themes` 폴더에 있는 코드를 직접 수정하는 것보다는, 원래 테마 코드는 그대로 보존한 채 root 폴더 내에 `themes` 구조를 복사해서 수정하는 것이 좋다고 한다. 테마에 관한 다른 커스터마이징에도 똑같이 해당된다(나는 이미 원래 코드를 많이 바꿔버렸지만).

2. `{{ template "_internal/google_analytics.html" . }}`를 추가한다

내가 참고한 글과 내 블로그의 config가 다르게 생겨서 임의로 비슷한 위치에 추가했다.

```
<header class="intro-and-nav" role="banner">
  <div>
    <div class="intro">
      <a class="logo" href="/" aria-label="{{ .Site.Title }} home page">
        <img src="{{ "images/logo.svg" | absURL }}" alt="">
      </a>
      <p class="library-desc">
        {{ with .Site.Params.description }}
          {{ . | markdownify }}
        {{ end }}
      </p>
    </div>
    {{ partial "nav.html" . }}
      {{ template "_internal/google_analytics.html" . }}
  </div>
</header>
```

### local 서버 접속은 제외하기

로컬 서버 접속 여부는 별로 궁금하지 않다. 혹시 `cupper-hugo-theme`과 다르게 local 서버 접속이 모니터링 대상에 포함되어 있어서 이를 제외하고 싶다면 내가 사용한 `cupper-hugo-theme`와 같이 `/layouts/partials/google-analytics-async.html`에 `{{ if not .Site.IsServer }}`와 `{{ end }}`를 추가해도 될 것 같다.

혹은 아래 과정을 참고해본다.  
[이 답글](https://discourse.gohugo.io/t/how-to-exclude-google-analytics-when-running-under-hugo-local-server/6092/34)을 참고해서 `header.html`을 다음과 같이 수정한다:

```
<header class="intro-and-nav" role="banner">
  <div>
    <div class="intro">
      <a class="logo" href="/" aria-label="{{ .Site.Title }} home page">
        <img src="{{ "images/logo.svg" | absURL }}" alt="">
      </a>
      <p class="library-desc">
        {{ with .Site.Params.description }}
          {{ . | markdownify }}
        {{ end }}
      </p>
    </div>
    {{ partial "nav.html" . }}
    {{- if not .Site.IsServer -}}
      {{ template "_internal/google_analytics.html" . }}
    {{- end -}}
  </div>
</header>
```

## 후기

테마 제작자가 열일해준 덕분에 추정 ID 입력만으로도 작업이 얼추 끝났다.

하지만 이상한 점이 있다. 처음 접속할 때 현재 접속자 수가 0명에서 1명으로는 잘 바뀌는데, 창을 닫아도 다시 0명으로는 잘 바뀌지 않을 때가 있다.

그리고 로컬 서버뿐만 아니라, `https://<username>.gitub.io`도 모니터링 대상에서 제외하고 싶다.
만약 내가 고정 ip주소를 사용한다면 GA 자체 필터링 기능으로 내 ip 주소를 보고서에서 제외할 수 있다(수집은 되지만 보고서에서만 제외되는 것). 자세한 건 [여기](https://blog.fakecoding.com/2019/03/28/%EA%B5%AC%EA%B8%80-%EC%95%A0%EB%84%90%EB%A6%AC%ED%8B%B1%EC%8A%A4-%EB%82%B4-%EC%A0%91%EC%86%8D-%EA%B8%B0%EB%A1%9D-%EC%A0%9C%EC%99%B8/)를 참조. 하지만 나는 주로 카페 와이파이를 사용하니까 고정 ip가 아닌 것 같다.

일단은 이대로 두자. GA가 내 블로그에서 딱히 의미 있는 기능이 될 것 같지는 않으니.

## References

- [Setting Up Google Analytics on Hugo](http://cloudywithachanceofdevops.com/posts/2018/05/17/setting-up-google-analytics-on-hugo/)
- [[GA] 구글애널리틱스 시작, 계정 생성하고 추적코드 설치하기](https://ga-study.tistory.com/4)
- [How to Exclude Google Analytics When Running Under Hugo Local Server](https://discourse.gohugo.io/t/how-to-exclude-google-analytics-when-running-under-hugo-local-server/6092/34)