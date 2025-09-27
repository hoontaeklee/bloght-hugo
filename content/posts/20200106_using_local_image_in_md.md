---
title: Hugo 블로그 게시글에 첨부한 로컬 이미지가 안 보일 때
author: "Hoontaek Lee"
date: 2020-01-06 11:11:00+09:00
publishdate: 2020-01-06 20:59:44+09:00
lastmod: 2020-01-06 22:09:44+09:00
tags:
- Hugo
- Blog
- 2020
categories:
- Blog Maintenance
draft: false
---

## 해답은 이미지 주소를 올바르게 참조하는 것

> Hugo 게시판에 올린 [질문](https://discourse.gohugo.io/t/image-is-not-shown-or-broken-on-webpage/22584)

블로그에 게시글 올릴 때, 게시글에 이미지를 자주 사용하게 된다.  

마크다운으로 글을 작성할 때 해당 이미지의 **인터넷 주소** 를 참조하거나, 혹은 이미지를 폴더에 저장한 후 저장한 **폴더의 주소** 를 참조한다.  

처음에 이런 방법으로 이미지를 첨부했는데, 마크다운 에디터 미리보기에서는 그 이미지가 보이지만 정작 웹페이지에서는 안 보이는 문제가 있었다.

답변을 참조하면서 이리저리 해보다가 **working solution** 을 찾았다. 바로 1) 블로그 root directory와 그 하위 폴더는 주소에서 제외하는 것, 그리고 2) **/** 로 시작하는 것이다.

**예를 들어** 내 이미지 `A.jpg`의 주소가 `blogRoot/static/images/A.jpg`라면, 마크다운에서 참조할 때는 `/images/A.jpg`와 같이 사용하는 것이다. 마찬가지로, 이미지 `article_B.jpg`의 주소가 `blogRoot/content/post/article_B/B.jpg`라면, 마크다운에서는 `/post/article_B/B.jpg`라고 써준다. 만약 `blogRoot/content/image.jpg`에 있다면, `/image.jpg` 처럼 써 준다.

`blogRoot`에 있는 이미지를 참조하는 경우는 거의 없을 것 같으니 생략한다.  

이미지뿐만 아니라, `pdf` 등 다른 형식의 로컬 파일을 참조할 때도 마찬가지 규칙을 적용하면 된다.

하지만 왜 이렇게 하면 작동하는지는 잘 모르겠다.

### 누군가 Hugo 게시글에 [답변](https://discourse.gohugo.io/t/image-is-not-shown-or-broken-on-webpage/22584/12)을 올려줬다

#### Root가 `public`으로 바뀌기 때문!

Hugo가 웹페이지를 만들면서 `content`와 `static`의 하위 내용이 `public`에 저장된다. 그리고 `public`은 새로운 `root`가 된다. 즉, 내가 언급한 `blogRoot`의 바로 하위폴더 레벨의 폴더들이 `public`으로 옮겨지게 되는 셈이고 때문에 `/`로 시작하면 `public` 내 파일에 접근할수 있는 것이다.

위의 `A.jpg` 예를 보면, 원래 주소가 `blogRoot/static/images/A.jpg`였는데, 웹페이지를 만들면 `static`의 하위 폴더인 `images`는 `public`으로 복사되어 `/public/images/A.jpg`의 주소로 바뀌게 된다. 때문에 `/images/A.jpg`와 같이 접근하는 것이다.  

참고로 내가 실패했을 때는 `A.jpg`, `static/images/A.jpg` 등을 사용했었다.
