---
title: Hugo를 이용해 Github 저장소에서 블로그용 정적 웹페이지 만들기
author: "Hoontaek Lee"
date: "2019-12-29 04:17:00+09:00"
publishdate: "2020-01-01 13:37:00+09:00"
lastmod: "2020-01-01 17:00:00+09:00"
tags:
- Hugo
- GitHub
- Blog
- 2019
categories:
- Blog Maintenance
draft: false
---

<!--
## 목차

- [설치](#%EC%84%A4%EC%B9%98)
- [웹사이트 생성](#%EC%9B%B9%EC%82%AC%EC%9D%B4%ED%8A%B8-%EC%83%9D%EC%84%B1)
- [테마 적용](#%ED%85%8C%EB%A7%88-%EC%A0%81%EC%9A%A9)
- [원격 저장소 세팅](#%EC%9B%90%EA%B2%A9-%EC%A0%80%EC%9E%A5%EC%86%8C-%EC%84%B8%ED%8C%85)
- [포스팅 & 호스팅](#%ED%8F%AC%EC%8A%A4%ED%8C%85--%ED%98%B8%EC%8A%A4%ED%8C%85)
- [Trouble Shooting](#trouble-shooting)
- [Reference](#reference)

-->

## 설치

#### Git 설치

1. [Git 홈페이지](https://git-scm.com/) 오른쪽 아래 초록 링크
2. cmd에서 버전 잘 나오나 확인
```
$ git --version
```

#### Hugo 설치
[Hugo 웹페이지](https://gohugo.io/getting-started/installing/#windows) 참고  

1. C드라이브에 Hugo 폴더 생성(블로그 관련 파일 저장용)
2. Hugo 폴더 안에 bin 폴더 생성(Hugo 관련 파일 저장)
3. [Hugo 깃허브 저장소](https://github.com/gohugoio/hugo/releases)에서 최신 릴리즈 압축파일 다운로드
4. `C:/Hugo/bin`에 압축 해제
5. 환경변수에 `C:/Hugo/bin`추가
  - 윈도우 10: [여기](https://gohugo.io/getting-started/installing/#for-windows-10-users)를 참고
    - 윈도우키 - "환경" 검색 - "계정의 환경 변수 편집" - 유저 변수에서 `Path` 더블클릭 - 새로만들기 - `C:/Hugo/bin`입력 - 확인
  - 환경변수를 추가하면 `C:/Hugo/bin` 외의 경로에서도 `C:/Hugo/bin`의 `hugo.exe` 사용 가능(= Hugo 사용 가능)
6. 설치 확인
  - `cmd`에서 버전 정보 나오는지 확인
```
Hugo version
```

## 웹사이트 생성
  - 블로그 담을 폴더 생성(`\C:\Users\Owner\Dropbox\bloght`)
    
    - 아무 경로 가능, 한글은 피하는 게 좋을 듯
  - `cmd`에서 해당 경로로 이동 후
       ```
       hugo new site bloght
       ```
       `bloght` 폴더에 Hugo 웹사이트로서 기능하기 위한 정보가 추가된다.

## 테마 적용

#### 1. 블로그 폴더를 git 저장소로 변경

  - 생성한 블로그 폴더에서 아래 명령 실행:
      ```
      git init
      ```
`git init`을 실행하면 `git` 저장소를 위한 기본 정보를 담고 있는 `.git` 디렉토리가 만들어진다. 즉, `git init`는 일반 저장소를 git 저장소化하는 셈이다.

#### 2. 테마 선택 및 사용
  - `https://themes.gohugo.io/`에서 테마 선택
  - 내가 고려한 것
    - 메인페이지로 시작, blog/about/tag(or category) 페이지로 넘어갈 수 있는
    - 포스팅 작성 날짜 및 시간을 볼 수 있는 (yyyy-mm-dd hh:mm:ss)
    - 한글 지원이 잘 되는(+폰트)
    - dark/light 전환 가능한
    - 모바일에서도 잘 보이는
    - `cupper-hugo-theme`, `kiss`, `vanilla-bootstrap-hugo-theme`, `hugo-theme-yuki`
  - 테마 사용: `cmd`에서 블로그 폴더(`bloght`)로 이동 후 아래 명령 실행:
      ```
      git submodule add https://github.com/zwbetz-gh/cupper-hugo-theme.git themes/cupper-hugo-theme
      ```
    - `git submoduel add`: 테마를 submodule 형태로 git 저장소에 추가
    - `https://github.com/zwbetz-gh/cupper-hugo-theme.git`: 선택한 테마의 git 저장소 주소
    - `themes/cupper-hugo-theme`: 블로그 폴더(`bloght`)의 `theme`폴더에 선택한 테마의 이름으로 폴더를 만들어 관련 정보를 저장
  - config 파일 설정
    - 아까 `hugo new site bloght` 명령을 통해 `bloght`를 블로그 저장소로 만들었는데, 이 때 블로그 세팅 정보가 담겨 있는 `config.toml` 파일이 생성됐었다.
    - `theme`의 `exampleSite` 폴더에 있는 `config.toml` (or `config.yaml`) 파일과 `content` 폴더를 `bloght`로 복사한다.
    - 내가 선택한 테마가 `config.yaml`를 사용할 경우 기존 `bloght`의 `config.toml`은 없애준다(에러나더라. 충돌하는 듯?)
    - config.toml의 `theme` 변수를 선택한 테마 이름으로 변경해준다(직접 해도 되고, 명령어로도 가능:
      ```
      echo `theme = "cupper-hugo-theme"` >> config.yaml
      ```
  - baseURL (--> "https://username.github.io"), 블로거 이름 등 바꿔준다.
  - 기타 커스터마이징하고 싶으면 exampleSite의 config파일 구조를 분석하거나 구글링.

## 원격 저장소 세팅

#### 1.저장소 2개 생성

- 한 개: 블로그 컨텐츠 담는 용도. **anyblogname**: `bloght`
- 한 개: 렌더링 된 웹사이트 담는 용도(`public` 폴더의 내용). **username.github.io** 형식: `bloght.github.io`
- Initialize with README 체크 - 하든 말든 상관 없다.

#### 2. 로컬 저장소와 연동

- 로컬 저장소와 원격 저장소를 연동한다:
   ```
   git remote add origin https://github.com/hoontaeklee/bloght.git
   ```
- 현재 원격 저장소는 빈 상태이므로 로컬 저장소의 내용을 복사해준다:
  ```
  git push origin master
  ```

#### 3. Submodule 추가

- 기존에 생성했던 public 폴더는 지운다:
  ```
  rm -rf public
  ```
- `hoontaeklee.github.io` 저장소를 `bloght` 저장소의 submodule로 추가 한다:
  ```
  git submodule add -b master https://github.com/hoontaeklee/hoontaeklee.github.io.git public
  ```
  - `bloght`의 public 폴더가 `hoontaeklee.github.io` 저장소로 분리, 독립된다.
  - 가끔 [에러](#2-unable-to-checkout-submodule-public)가 난다.

## 포스팅 & 호스팅

#### 1. 컨텐츠 생성

  - 로컬에서 웹사이트를 미리 볼 수 있다(http://localhost:1313):
      ```
      hugo server
      ```
    - 컨텐츠 내용을 바꿀 때마다 자동으로 감지 및 반영해주기 때문에 유용하다.

#### 2. 컨텐츠 업로드
  - 로컬에서 웹사이트 빌드 --> 저장소 두 개 업데이트 순서로 진행된다.
아래 명령어를 사용한다:

```
# site build
hugo -t cupper-hugo-theme

# username.github.io 업데이트
cd public
git add .
git commit -m "commit message"
git push origin master

# anyblogname 업데이트
git ..
git add .
git commit -m "commit message"
git push origin master
```
- 빌드 명령어에 테마 이름이 들어간다: themes 폴더에 여러 테마 받아 놓고 **원하는 테마 선택해서 빌딩 가능**.
- 매번 위 명령어를 통해 업데이트할 수도 있지만, 아래처럼 쉘스크립트로 한 번에 할 수도 있다.  
  - deploy.sh 파일을 ``bloght`` 폴더에 생성한 후 아래 내용을 붙여 넣는다:

```
#!/bin/sh

# If a command fails then the deploy stops
set -e

printf "\033[0;32mDeploying updates to GitHub...\033[0m\n"

# Build the project.
hugo # if using a theme, replace with `hugo -t <YOURTHEME>`

# Go To Public folder
cd public

# Add changes to git.
git add .

# Commit changes.
msg="rebuilding site $(date)"
if [ -n "$*" ]; then
	msg="$*"
fi
git commit -m "$msg"

# Push source and build repos.
git push origin master

# anyblogname 업데이트
git add .

msg="rebuilding site `date`"
if [ $# -eq 1 ]
  then msg="$1"
fi
git commit -m "$msg"

git push origin master
```

- 이제 명령어 한 줄만으로 build & push할 수 있다:
```
./deploy.sh "commit message"
```

- 가끔 잘 안 된다: 내가 변경한 파일이 untracked file이어서 Github로 push가 안 된다. 이럴 때는 수동으로 해주면 된다.

## Trouble Shooting

#### 1. push - Permission denied (publickey)
```
$ git push -u origin master
Warning: Permanently added the RSA host key for IP address '15.164.81.167' to th     e list of known hosts.
git@github.com: Permission denied (publickey).
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
```
##### 정황
- 로컬 블로그 저장소를 생성한 깃허브 저장소에 푸쉬할 때 위의 에러가 발생했다.
- 깃허브 주소는 두 가지 방법(`SSH` vs `HTTPS`)으로 표현할 수 있다. `git remote -v`를 통해 현재 로컬 저장소를 원격 저장소에 연결할 때(remote) SSH 방식의 주소를 사용하고 있음을 확인했다.

##### 해결
- [여기](https://help.github.com/en/github/using-git/changing-a-remotes-url)를 참고해서 `remote`의 url을 `SSH`에서 `HTTPS`방식으로 변경하니 푸쉬 성공(해결 원리는 잘 모르겠다)

#### 2. Unable to checkout submodule 'public'
```
$ git submodule add -b master https://github.com/hoontaeklee/hoontaeklee.github.io.git public
warning: You appear to have cloned an empty repository.
fatal: 'origin/master' is not a commit and a branch 'master' cannot be created from it
Unable to checkout submodule 'public'
```
##### 정황
- 웹사이트 저장소를 컨텐츠 저장소의 submodule로 추가할 때 에러 발생

##### 해결
- `https` 주소를 `ssh` 주소로 바꿔서 해결했다(원리는 모르겠다. `remote` 연결은 `https`로 했었는데.)

## Reference
- [Hugo: Quick Start](https://gohugo.io/getting-started/quick-start/)
- [Hugo: Host on Github](https://gohugo.io/hosting-and-deployment/hosting-on-github/)
- [Hugo로 Github.io 블로그 만들기](https://github.com/Integerous/Integerous.github.io/blob/master/README.md)
- [블로그 구축기 1 (Hugo + github.io)](https://ialy1595.github.io/post/blog-construct-1/)
- [Creating a Hugo Site on Github Pages](https://dev.to/dgavlock/creating-a-hugo-site-on-github-pages-3cjo)
