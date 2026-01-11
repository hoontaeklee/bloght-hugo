---
title: "Dropbox - RStudio- Github 연동 : 더 편해졌을까?"
author: "HoonTaek Lee"
date: 2019-12-08 16:42:00+09:00
publishdate: 2020-01-01 14:16:00+09:00
lastmod: 2020-01-01 14:14:00+09:00
draft: false
tags:
- Hugo
- Blog
- 2019
series:
-
categories:
- Blog Maintenance
image:
---

## 2019. 12. 08.

하루 하나씩 Dropbox에 저장된 서평(.docx)을 블로그에 옮기고 있다. 
옮기는 방식은 다음과 같다 :  
1. Git의 블로그 저장소에 .md 파일 생성
2. 옮기려는 워드 파일을 열어서 내용 복붙
3. 오타, 문장 수정 & Preview를 보며 문장, 문단 배치 수정
4. 표(저자, 제목, 출판일, 읽은 날짜 등)와 책 그림 추가
5. Medium Story로 Publish

조만간 논문 리뷰(.Rmd)도 Medium에 옮기려 한다. 논문 리뷰는 RStudio에서 작업하고 Rmd 파일로 저장한다. 이전에 `blogdown` 라이브러리 사용할 때 RStudio와 Github 저장소를 연동했던 것이 떠올랐다. 지금 블로그도 연동해두면 뭔가 편해질 것 같았다. [이 글]( https://uang.tistory.com/11)을 참고해서 일단 해봤다.

  - RStudio - new project - version control에서 기존 github에 있던 블로그 저장소 url을 따온다
  - 폴더 생성 위치를 내 Dropbox로 지정한다

이렇게 하면 Github의 원격 저장소(내 컴퓨터에 없고 Github에 있으니까 원격이다)로 존재하던 블로그 폴더를  
Dropbox에 로컬 저장소(=탐색기에서 보이는 폴더)로 통째로 옮겨오게 된다.

이제 RStudio에서 쓴 글을 Github와 Dropbox에 반영할 수 있고, 그 반대도 가능하다.

  - 로컬 --> 원격 : commit + push
  - 원격 --> 로컬 : pull

다만, 여전히 몇 가지 이슈가 있다.

  - 에디터마다 장단점이 서로 다르다
    - RStudio : Rmarkdown, R code 작성은 쉽지만 preview가 불편하다
    - Git : R code를 작성하기 힘들다(불가능하다?). 대신 markdown은 바로바로 렌더링해주기 때문에 편하다
    - Medium : 게시글이 어떻게 보일지 글을 작성하면서 볼 수 있다. 하지만 Rmarkdown, markdown 다루기는 제일 불편하다

  - 그래서 무엇이 편해졌는지 잘 모르겠다
    - 쓰면서 알아보자
    - 일단은 version control을 사용한다는 것에 의의를 두자

## 2020. 01. 01.

지금은 `Medium`이 아닌, `Github`와 `Hugo`를 이용하는 플랫폼을 시험해보고 있다.  
이 방법에서는 `Github` 저장소로 블로그가 백업되는데, `Dropbox`와 연동하면 백업을 한 번 더 할 수 있다는 장점이 있다. 다만, `RStudio`와 연동하는 것은 아직까지 큰 장점이 없다. 마크다운 에디터로 사용하는 것도 아니고. 만약 `R` 코드가 내용이 포함된다면 장점이 있을지도 모르겠다.
