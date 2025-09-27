---
title: "How to switch to another Hugo theme (Hugo 테마 변경하기)"
author: "Hoontaek Lee"
date: 2020-02-15 15:09:56+09:00
publishdate: 2020-02-15 15:09:56+09:00
lastmod: 2020-02-15 15:09:56+09:00
tags:
- Hugo
- Blog
- 2020
categories:
- Blog Maintenance
draft: false
---

# Intro

Hugo theme 목록에 마음에 드는 테마가 올라왔다. 기존에 사용하던 [Cupper](https://github.com/zwbetz-gh/cupper-hugo-theme) 테마에서 [Zzo](https://themes.gohugo.io//theme/hugo-theme-zzo/en/) 테마로 바꾸기로 했다. 이유는 굳이 따지지 않는다. 그냥 바꾸고 싶은 거다. 

Zzo 테마는 **예쁘고**, 기능도 **있을 것 다 있고**(맨 위로 가는 버튼, 이전/다음 게시글 이동 버튼 등), **없을 기능도 있고**(Resume page, publication page, ...), **[메뉴얼](https://zzodocs.netlify.com/)도 잘 돼있다**. 

어떻게 바꿔야 할까.



# Plan

**처음에는** Cupper와 zzo 모두 설치해놓고 언제든 이 테마에서 저 테마로 스위치 누르듯 옮길 수 있으면 좋겠다고 생각했다. 내가 쓰고 있는 Cupper는 오리지널 버전을 조금 수정한 것이기 때문이다. **삽질한 게 얼만데.** 

**현재 내 테마 폴더 구조는**... Cupper 오리지널 버전을 `/themes/Cupper-hugo-theme`에 `submodule`로 저장해놓고 테마 구조를 `root`에 복사하여 overriding(같은 이름이면 root에 있는 코드가 우선 적용되는 것)해 사용하고 있는 상태다. 처음 구상했던 방법으로는 `themes`안에 있는 것은 여러 테마를 보전할 수 있다 쳐도, **`root`에 overriding해놓은 것은 어떻게 살릴지** 감이 안 왔다. Hugo에 물어봤다.

결국, **기존 테마를 지우고 새로 테마를 설치**하기로 했다. 운 좋게도 **zzo님이 직접 [답변](https://discourse.gohugo.io/t/how-to-save-the-customized-theme-before-applying-another-theme/23321/4)**을 해주셨다. **요약**하면, 1) 내 상상은 상상에 불과했고, 2) 테마는 하나만 설치하는 게 좋다(테마마다 세부 구조가 서로 다르기 때문에 서로 충돌할 수 있음), 3) 내가 상상한 여러 테마를 왔다갔다하는 방법은 어떻게든 실현 가능하겠지만 에러 날 확률이 높다는 내용이었다. 깔끔하게 새로 테마 하나를 깔기로 했다.

0. **메뉴얼 읽기** : [설명서](https://zzodocs.netlify.com/)를 읽으면 어떻게 할지, 어떤 문제가 생길 수 있을지 감이 좀 오겠지.

1. **컨텐츠 백업** : 가장 중요하다. 컨텐츠만 있으면 블로그 하나 다시 만들어서라도 복구가 가능하다. 나는 블로그 폴더를 **Dropbox**에 저장해놓으니 백업 문제는 자동으로 해결된 듯하다.
2. **테마 삭제** : 깔끔하게 지우는 방법이 따로 있을까 찾아봤더니 잘 안 나온다. 내 로컬 블로그 폴더에서만 지우기로 했다.
3. **테마 설치** : [기존에 썼던 글](/en/posts/20191229_blogging_with_hugo.md)의 **테마 적용** 부분부터 따라해보려 한다. **블로그 만들 때와 다른 점**(내 로컬 폴더는 이미 `git init` 된 상태, `hoontaeklee.github.io` 저장소는 이미 `submodule`로 추가된 상태 등)이 있다는 걸 고려하며 참고한다.



# Action

0. **메뉴얼 읽기** : 메뉴얼은 **설치**(Getting Started), **페이지 관련 세팅**(Pages), **기타 세팅**(Configuration), Shortcodes, **Customization**, **External Libraries**로 구성된다. 그렇게 길지 않고 필요한 부분을 쉽게 찾을 수 있게 돼 있다.

   

1. **컨텐츠 백업** : Dropbox

   

2. **테마 삭제** :

   1. Cupper와 zzo 공통으로 일곱 개 폴더를 가지고 있다(archetypes, assets, data, exampleSite, images, layouts, static).

   2. zzo는 `i18n` 폴더(언어 설정 관련?)를 추가로 가지고 있다.

      

3. **테마 설치** : 

   1. 테마 다운로드

      Hugo 메뉴얼에도, 테마 메뉴얼에도 같은 코드를 알려준다.
      ```
      git submodule add https://github.com/zzossig/hugo-theme-zzo.git themes/zzo
      ```
      위 코드를 Git bash나 cmd를 이용해 블로그 폴더에서 실행한다.    
      
      
      
   2. 폴더 구조 수정

      테마를 다운받으면, `themes/zzo` 와 `exampleSite` 폴더를 `root`로 복사한다. **Overriding**하는 것인데, **원래의 테마 코드를 건들지 않고** 내 입맛에 맞게 테마를 수정할 수 있다. 

      **주의할 것**은, 내 질문에 zzo님이 답변한 것처럼 **테마 구조가 조금씩 다르다**. 예를 들어 Cupper 테마는 `post`폴더지만, zzo는 `posts` 폴더다. 그리고 `post` 폴더 구조도 Cupper는 바로 게시글이나 그림이 들어가는 반면, zzo는 다중 언어 사용을 지원하기 때문에 `en`, `ko` 언어별 폴더가 있고 각 폴더 안에 게시글 관련 파일이 담겨있다. 그리고 Cupper는 `config.toml`만 덩그러니 있는 반면, zzo는 `config` 폴더가 따로 있어서 이 안에 config.toml 파일이 들어있다.

      이런 다른 점까지 모두 **똑같이 맞춰줘야** 오류가 없다. 

      

      3. 기타 수정할 것들

         - `deploy.sh` 파일(포스팅 자동화한 배쉬 파일) 안에서 사용할 테마 이름을 zzo로 바꿔준다.

         - **front matter** : 이거야말로 테마마다 가지각색이다.

           

      4. 반영하기

         맨 처음 블로그 만들 때 했던 것처럼 `deploy.sh` 내용을 한 번 단계별로 실행하면서 문제가 없는지 살펴본다.

         ```hugo &amp; git
         # site build
         hugo -t zzo
         
         # username.github.io 업데이트
         cd public
         git add .
         git commit -m "commit message"
         git push origin master
         
         # anyblogname 업데이트
         git ..
         git add .
         git commit -m "commit message"
         git push 
         ```
         
         
         
         **!!!!!!!!!!!!!!!!!**
         
      - origin mastersite build 후에는 **몇분 기다려야** 한다(게시글이 많을 수록 더 오래 걸린다). 
           누구처럼 404 Not Found 에러보고 이것저것 삽질하지 말자.
         
         - **에러**
           메세지 : TOCSS: failed to transform ~~        
           해결 : hugo extended version을 설치한다. 방법은 [여기](https://gohugo.io/getting-started/installing/#chocolatey-windows). **재부팅 필요**
         
           
      
# Close

어찌어찌 뼈대는 완성됐다. 이쁘군.

**관건은 테마 구조 똑같이 맞춰주기**였다.

검색엔진노출 설정, Google Analytics 설정만 아니었으면 블로그 하나 다시 만드는 게 나을지도 모르겠다(별 거 아니라 생각되면 그냥 저 두 개도 새로 해도 되겠다).

