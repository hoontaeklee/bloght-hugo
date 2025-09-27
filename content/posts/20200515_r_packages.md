---
title: "R packages by Hadley Wickham 정리"
author: "Hoontaek Lee"
date: 2020-05-12T10:00:00+09:00
lastmod: 2020-05-15T19:18:00+09:00  
description:
draft: false
hideToc: false
enableToc: true
enableTocContent: false
tocPosition: outer
tocLevels: ["h2", "h3", "h4"]
tags:
- 2020
- Book Review
- R
---

# Getting started
## Introduction 

### 패키지를 만드는 이유

* 다른 사람과 코드 공유
* **다른 사람들이** 내 코드를 쉽게 이해하고 사용할 수 있게 매뉴얼 작성
* **나 자신이** 내 코드를 쉽게 이해하고 사용할 수 있게 매뉴얼 작성

### Getting started

필요한 패키지&함수를 설치한다.

```r
install.packages(c("devtools", "roxygen2", "testthat", "knitr"))
```

올바른 버전의 패키지를 설치했는지 확인한다(TRUE가 나와야 함).

```r
install.packages("rstudioapi")
rstudioapi::isAvailable("0.99.149")
```


```r
devtools::install_github("r-lib/devtools")
```

필요한 것 모두 설치됐는지 확인한다.  
아래 코드 수행 결과 **TRUE**가 나오는지 확인한다.

```r
library(devtools)
has_devel()
```
## Package structure

* 패키지를 만드는 과정
* 패키지와 라이브러리의 차이점

### Naming your package

#### Requirements for a name

1. 문자, 숫자, 마침표로 구성
    - 문자로 시작해야 하고, 마침표는 마지막에 올 수 없다.
    - 되도록 마침표는 쓰지 말자.
    
#### Strategies for creating a name

* 유니크한 이름: 구글링 쉽게 되도록
  - [CRAN](https://cran.r-project.org/web/packages/available_packages_by_name.html)에서
  해당 패키지가 이미 존재하는지 확인하기
* 대소문자 섞지 말기: 타이핑, 기억 어렵다
  - RGtk2
* 패키지의 기능을 쉽게 연상할 수 있는 이름
  - lubridate: date와 times 다루기 쉽게하는(lubricate)
* 축약형(abbreviation) 사용
* r 추가해주기
  - stringr, readr, gistr, ...
* 상용 패키지를 개발할 경우, 해당 회사의 가이드라인 숙지하기
  - Dropbox는 브랜드 이름으로 어플리캐이션을 만들지 못하게 한다. 그래서 rDropbox가 아닌 rDrop이 되었다.

#### Creating a package

이름을 지었다면 새 패키지를 만들어보자.  
**두 가지 방법**이 있는데, **모두 RStudio에서 진행 가능하다.**

1. RStudio - File - New Project - New Directory - R package - 이름 입력 후 Create Project
2. 아래 코드를 실행한다:
`devtools::create("path/to/package/pkgname")`

두 방법 모두 실행 결과는 같다.  
위에서 보듯, 패키지 하나를 하나의 프로젝트로 간주한다.  
**가장 단순한 구성의 패키지(the smallest usable package)**를 생성한다. **세 가지 요소**로 구성된다.

1. [`R/` 폴더](http://r-pkgs.had.co.nz/r.html#r)
2. [`DESCRIPTION` 파일](http://r-pkgs.had.co.nz/description.html#description)
3. [`NAMESPACE` 파일](http://r-pkgs.had.co.nz/namespace.html#namespace)

이와 함께, RStudio에서 작업하기 수월하도록 `pkgname.Rproj`도 생성된다.

```
# 주의
package.skeleton() 함수로 패키지 생성지 말 것!  
위 함수는 지금 필요한 것보다 많은 것을 만들기 때문에 추후 작업량이 늘어날 수 있다.
```

#### RStudio projects

패키지를 하나의 프로젝트로 분리하면 여러 **장점**이 있다.

1. 다른 프로젝트와 독립적: 서로 코드 영향 없음
2. 다양한 단축키 사용 가능(`Alt + Shift + K`)

`pkgname.Rproj` 파일은 `devtools::use_rstudio("path/to/package")` 명령어로 생성할 수 있다.

##### What is an RStudio project file?

`devtools`가 만들어내는 **텍스트파일**이다.  
관련 옵션은 RStudio - Projects Options...에서 변경 가능하다.


##### What is a package?

간단한 패키지 생성에는 위의 내용으로 충분하지만,  
패키지를 배포할 때 **패키지의 다섯 가지 상태**를 알아두면 도움이 될 것이다.  

* Lifecycle of a package
  1. source
  2. bundled
  3. binary
  4. installed
  5. in-memory

###### Source packages

아직 개발 진행중인, 내 컴퓨터에 저장돼있는 것들이다.  
위에서 생성한 `R/` 폴더, `DESCRIPTION` 파일 등이다.

###### Bundled packages

> A bundled package is a package that’s been compressed into a single file.

하나의 파일로 압축된 형태.  
리눅스에서는 `tar.gz` 확장자를 사용한다. 하나의 파일로 묶어서(`.tar`) gzip으로 압축했다는 (`.gz`) 뜻이다.
**`devtools::build()`로 생성한다.**

압축 해제한 Bundled package와 source package의 차이는 아래와 같다:
  - Bp에는 Vignettes가 있다(덕분에 html, PDF 생성 가능).
  - Bp에는 개발 중 생성된 임시파일(컴파일 관련 등)이 없다.
  - Bp에는 `.Rbuildignore`에 적혀있는 것들이 없다.

`.Rbuildignore`이란...
  - source에는 있어야 하지만 bundle에는 없어야 할 때 명시해주면 좋다(데이터 등)
  - **Perl 유형의 정규표현식**을 사용한다.
  - 한 행에는 한 가지 예외 사례를 적는다.
  - 특정 파일이나 폴더를 제외하고 싶을 때, **그 이름을 그대로 쓰면 안 된다.**
    - notes를 제외하고 싶다면 `^notes$` 혹은 `devtools::use_build_ignore("notes")`를 사용한다.
    - **notes를 사용하면** 이름에 notes가 포함된 모든 파일이 제외된다.

Hadley의 예시:

```
^.*\.Rproj$         # Automatically added by RStudio,
^\.Rproj\.user$     # used for temporary files. 
^README\.Rmd$       # An Rmarkdown file used to generate README.md
^cran-comments\.md$ # Comments for CRAN submission
^NEWS\.md$          # A news file written in Markdown
^\.travis\.yml$     # Used for continuous integration testing with travis
```

###### Binary packages

> If you want to distribute your package to an R user who doesn’t have package
development tools, you’ll need to make a binary package.

Package development tools를 가지고 있지 않은 유저에게 배포할 때는 Binary 형태로 만들어야 한다.  

A package bundle과 마찬가지로 **하나의 파일로 압축된 형태**지만,  
(bundle과 달리) 압축을 해제했을 때 source와는 내부 구조가 다르다:

- `R/` 폴더에 `.R` 파일이 없다.
- `Meta/` 폴더에 `Rds` 파일이 들어있다. 
  - 패키지 설명 등
  - `readRDS()`로 읽을 수 있다.
- `html/` 폴더
  - HTML 형식의 도움말
- `src/`에 있던 코드는 `libs/`에 저장된다.
  - 32비트는 `i386/`, 64비트는 `x64/`
- `inst/`가 최상위 경로에 위치한다.

Binary는 **플랫폼 간 호환이 안 된다.**  
Windows의 binary(`.zip`)는 macOS에서 안 열리고, 반대로 macOS의 binary(`tgz`)는 Windows에서 열 수
없다.

**`devtools::build(binary = TRUE)` 명령어로 생성한다.**

![](http://r-pkgs.had.co.nz/diagrams/package-files.png)

###### Installed packages

> An installed package is just a binary package that’s been decompressed into a
package library.

압축 해제한 binary.

지금까지 배운 바로는 source -> bundle / binary -> installed 순서로 배포를 진행하면 될 것 같다.
하지만 실제로는 더 다양한 방법으로 배포할 수 있다.

![](http://r-pkgs.had.co.nz/diagrams/installation.png)

> The tool that powers all package installation is the command line tool R CMD
INSTALL - it can install a source, bundle or a binary package.

**커맨드라인에서** `R CMD INSTALL`로 source, bundle, binary 설치 가능하다.
**R에서** 커맨드라인 명령어 실행할 수 있다:

  - `devtools::install()`: `R CMD INSTALL` 실행
  - `devtools::build()`: `R CMD build` 실행(source -> bundle)
  - `devtools::install_github()`: GitHub에서 source 다운로드 + vignettes 생성(`build()`)
  + install(`R CMD INSTALL`)
  - `install.packages()`, `devtools::install_url()`,
    `devtools::install_gitorious()`, `devtools::install_bitbucket()`
    - 모두 `devtools::install_github()`와 비슷한 역할을 한다.

`.Rinstignore`을 사용해 특정 파일 및 폴더를 install할 목록에서 뺄 수 있다(`.Rbuildignore`와 같은 방식).

###### In memory packages

패키지를 사용하려면 메모리로 불러들여야 한다(load).  
패키지 이름을 생략하려면(e.g. `devtools::install()` 대신 `install()), "search path"에 붙여야
한다(attach).
`library()` 함수로 loading + attaching을 수행할 수 있다.

```
# Automatically loads devtools
devtools::install()
    
# Loads and _attaches_ devtools to the search path
library(devtools)
install()
```

loading과 attaching은 패키지를 만들 때는 알아두는 게 좋다(단순 scripting할 때는 굳이 필요 없다).
뒤의 [search path](http://r-pkgs.had.co.nz/namespace.html#search-path) 챕터에서 자세히 다룰
예정이다.

패키지 유저는 `library()` 함수를 주로 사용하지만, **패키지 개발할 때는 그다지 유용하지 않다.** 그 패키지를 먼저 설치해야 하기
때문이다.
나중에 `devtools::load_all()` 명령어나, RStudio의 “Build and reload” 기능을 배울 것이다. 이를 통해
**설치하지 않고도 소스 코드를 메모리로 불러들일 수 있다.**

![](http://r-pkgs.had.co.nz/diagrams/loading.png)

##### What is a library?

> A library is simply a directory containing installed packages.

라이브러리 = 한 패키지의 폴더. 소스가 아닌 **installed package**를 담고 있는 폴더다.

R을 설치할 때 **자동으로 설치되는 것(e.g. base, stats, ...)**과 **사용자가 설치한 것**이 있다. R을 다시 설치할 때
사용자가 설치한 라이브러리를 잃어버릴 수 있다(하드드라이브에는 있지만 R이 찾지 못하는 것).

`.libPaths()` 명령어로 현재 사용하는 R에 설치된 라이브러리 목록을 볼 수 있다.

```
.libPaths()
#> [1] "/Users/hadley/R"                                               
#> [2] "/Library/Frameworks/R.framework/Versions/3.1/Resources/library"
lapply(.libPaths(), dir)
#> [[1]]
#>   [1] "AnnotationDbi"   "ash"             "assertthat"     
#>   ...      
#> [163] "xtable"          "yaml"            "zoo"            
#> 
#> [[2]]
#>  [1] "base"         "boot"         "class"        "cluster"     
#>  [5] "codetools"    "compiler"     "datasets"     "foreign"     
#>  [9] "graphics"     "grDevices"    "grid"         "KernSmooth"  
#> [13] "lattice"      "MASS"         "Matrix"       "methods"     
#> [17] "mgcv"         "nlme"         "nnet"         "parallel"    
#> [21] "rpart"        "spatial"      "splines"      "stats"       
#> [25] "stats4"       "survival"     "tcltk"        "tools"       
#> [29] "translations" "utils"
```
`.libPaths()` 실행 결과에서 [1]은 사용자가 설치한, [2]는 기본으로 설치되는 라이브러리의 경로다.

`library(pkg)` 또는 `require(pkg)` 명령어를 사용하면 R은 `.libPaths()`에서 해당 패키지가 있는지 검사한다.
만약 없다면 에러가 발생한다.

```
library(blah)

## Error in library(blah): there is no package called 'blah'

# or:
require(blah)

## Loading required package: blah
## Warning in library(package, lib.loc = lib.loc, character.only = TRUE,
## logical.return = TRUE, : there is no package called 'blah'
```

`library(pkg)`와 `require(pkg)`는 패키지를 발견하지 못 했을 때 대처 방식이 다르다.
`library()`는 에러를 발생시키는 반면, `require()`는 경고 메세지와 함께께 **FALSE**를 반환한다. **패키지 개발
중에는 소스코드에 절대로 `library(pkg)`나 `require(pkg)`를 사용하면 안 된다.** 대신 어떻게 해야 하는지는
[package dependencies](http://r-pkgs.had.co.nz/description.html#dependencies)를
참조.

# Package components
## R Code (`R/`)

### R code workflow

1. Edit an R file.
2. Press Ctrl/Cmd + Shift + L.
3. Explore the code in the console.
4. Rinse and repeat.

???

### Organising your functions

되도록 극단적인 방식은 피하자(한 파일에 모든 함수 때려넣기 또는 모든 함수마다 파일 따로 만들기).  
이름은 의미 있는 것으로 정하자.

> My rule of thumb is that if I can’t remember the name of the file where a
function lives, I need to either separate the functions into more files or give
the file a better name.

한 파일 내에서는 함수 위치가 그렇게 중요하지 않다. 단축키로 함수 사이를 넘나들 수 있기 때문이다.

- 에디터 내에서 함수 이름 클릭하고 `F2` 누르기
- `Ctrl + .` 누르고 함수 이름 검색하기

### Code style

> You don’t have to use my style, but I strongly recommend that you use a
consistent style and you document it.

그냥 유명한 거 쓰자([Hadley's style or [Google's R style
guide](https://google.github.io/styleguide/Rguide.xml)).

혹은 스타일링 함수를 사용해보자.

- `formatR` 패키지
```
install.packages("formatR")
formatR::tidy_dir("R")
```

- `linter` 패키지
```
install.packages("lintr")
lintr::lint_package()
```

### Top-level code

`source()`로 부를 수 있는 **scripts** vs. 패키지:

  * script를 읽어들이면 자동으로 실행된다. 패키지는 빌드만 된다(오브젝트 생성 = `.RData`를 읽어들이는 셈).
  * 패키지의 함수는 내가 모르는 상황에도 사용될 수 있도록 만들어야 한다(배포해야 하므로).

#### Loading code

`source()`로 스크립트를 불러들이면 즉시 실행된다. 반면, 패키지를 빌드할 때는 `R/`의 모든 코드가 실행되어 그 결과가 저장된다.
패키지를 load하면 빌드할 때 저장했던 결과만 메모리에 읽어들인다. 이를 스크립트로 표현하면 아래와 같다:

```
# Load a script into a new environment and save it
env <- new.env(parent = emptyenv())
source("my-script.R", local = env)
save(envir = env, "my-script.Rdata")

# Later, in another R session
load("my-script.Rdata")
```
다른 예를 들면, 만약 `x <- Sys.time()`을 스크립트에 저장하고 `source()`하면 스크립트가 실행되기 때문에
`source()`할 때의 시간이 `x`에 저장된다. 반면 패키지의 경우 `x`에는 빌드했던 시간이 기록돼있다(다시 실행하지 않기 때문).

This means that you should never run code at the top-level of a package.

```
# foo package

library(ggplot2)

show_mtcars <- function() {
  qplot(mpg, wt, data = mtcars)
}
```

위와 같이 코드를 작성하고 패키지로 만들어서 사용하면

```
library(foo)
show_mtcars()
```
에러가 발생한다. `foo`는 `library(ggplot2)`를 실행하지 않기에 `show_mtcars()`에 있는 `qplot()`이 실행될
수 없다.

아래와 같이 작성해도 문제가 발생한다.

```
show_mtcars <- function() {
  library(ggplot2)
  qplot(mpg, wt, data = mtcars)
}
```

따라서, `DESCRIPTION` 파일에 해당 패키지를 실행하기 위해 **필요한 라이브러리를 명시**해주는 게 좋다. [package
dependencies](http://r-pkgs.had.co.nz/description.html#dependencies)참고.

#### The R landscape

패키지는 내가 모르는 사람이 내가 모르는 상황, 환경에서 사용할 수 있다. 그러므로 내가 작성한 함수나 객체뿐만 아니라 **global
setting도 함께 고려해야** 한다. 즉, global setting을 함부로 변경시키는 코드를 패키지에 포함하면 안 된다(내 특정 상황에만
실행되는 코드가 만들어질 수 있다).

* `library()`나 `require()`를 사용하지 않는다. 이 두 함수는 search path를 바꾸기 때문에 해당 global
environment에서 사용할 수 있는 함수의 종류에 영향을 미친다.
* **절대로** `source()`를 사용하지 않는다(current environment가 바뀌게 된다). 대신,
`devtools::load_all()`를 사용하면 `R/`에 있는 모든 스크립트를 불러올 수 있다. Dataset을 만들고 싶다면
`data/`를 활용한다([datasets](http://r-pkgs.had.co.nz/data.html#data) 참고).
* global setting을 변경한 후에는 `on.exit()`를 이용해 **기본값으로 되돌려놓자**.

```
old <- options(stringsAsFactors = FALSE)
on.exit(options(old), add = TRUE)
```

```
old <- setwd(tempdir())
on.exit(setwd(old), add = TRUE)
```

* **plotting, printing**도 모두 global environment에 영향을 미친다. 각각 함수로 처리하면 해결할 수
있다(e.g. 데이터 가공 함수/그림 그리는 함수 따로 작성) .

반대로, 다른 사용자의 R environment에서만 구동되게 해서도 안 된다. 예를 들어, `read.csv()`의
`stringsAsFactors`를 패키지에서는 기본값인 `TRUE`를 사용했지만, 어떤 사람은 `FALSE`로 설정했을 수 있다.

#### When you **do** need side-effects

앞서서는 global environment를 건드리지 말라고 설명했지만,반대로 패키지를 사용하기 전에 **특정한 설정이 필요할 때**가 있다.
이 때는, `.onLoad()`나 `.onAttach()`를 사용할 수
있다([Namespaces](http://r-pkgs.had.co.nz/namespace.html#namespace) 참고). 특정 상황이
아니라면 `.onLoad()`를 사용하자.

`.onLoad()`와 `.onAttach()` 활용 사례

* 특정 메세지를 보여주고 싶을 때(startup messages): `.onAttach()` 사용

```
.onAttach <- function(libname, pkgname) {
packageStartupMessage("Welcome to my package")
}
```

* `options()`로 특정한 설정이 필요할 때: 옵션 설정하기 전에 내 패키지 이름을 prefix로 붙여주기 + 다른 사용자의 설정
override하지 않기.
* Hadley가 자주 쓰는 설정
```
.onLoad <- function(libname, pkgname) {
op <- options()
op.devtools <- list(
devtools.path = "~/R-dev",
devtools.install.args = "",
devtools.name = "Your name goes here",
devtools.desc.author = "First Last <first.last@example.com> [aut, cre]",
devtools.desc.license = "What license is it under?",
devtools.desc.suggests = NULL,
devtools.desc = list()
)
toset <- !(names(op.devtools) %in% names(op))
if(any(toset)) options(op.devtools[toset])

invisible()
}
```
* 다른 프로그래밍 언어를 사용할 때(e.g. cpp: `Rcpp::loadRcppModules()`)
* vignette engines을 등록할 때:`tools::vignetteEngine()`

`.onLoad()` 사용 후에는 `.onUnload()`로 해제해주자.
    
#### S4 classes, generics and methods

S4 클래스를 정의할 때도 environment를 건드려야 하며(generic, class 정의 ...), `DESCRIPTION` 파일의
`Collate` 변수를 활용할 수 있다. 자세한 내용은 [documenting
S4](http://r-pkgs.had.co.nz/man.html#man-s4)를 참고하자.

### CRAN notes

(매 챕터 마지막에 CRAN에 패키지를 등록하기 위한 팁을 마련했다. CRAN에 등록할 계획이 없다면 넘어가도 좋다.)

`.R`에 ASCII 문자만 사용하기!

`\u1234`와 같은 형식으로 유니코드를 사용할 수는 있다. 혹은 stringi::stri_escape_unicode()를 사용해도 된다:

```
x <- "This is a bullet •"
y <- "This is a bullet \u2022"
identical(x, y)
## [1] TRUE
```

```
cat(stringi::stri_escape_unicode(x))
## This is a bullet \u2022
```

## Package metadata (`DESCRIPTION`)

> Every package must have a DESCRIPTION. In fact, it’s the defining feature of a
package (RStudio and devtools consider any directory containing DESCRIPTION to
be a package).

`devtools::create("mypackage")`를 사용하면 간단한 description 파일이 생성된다:

```
Package: mypackage
Title: What The Package Does (one line, title case required)
Version: 0.1
Authors@R: person("First", "Last", email = "first.last@example.com",
                  role = c("aut", "cre"))
Description: What the package does (one paragraph)
Depends: R (>= 3.1.0)
License: What license is it under?
LazyData: true
```

패키지를 여럿 만들 때는 각 필드의 기본값을 설정할 수도 있다(`devtools.desc.author`,
`devtools.desc.license`, `devtools.desc.suggests`, `devtools.desc`).

`DESCRIPTION` 파일은 DCF(the Debian control format) 형식을 사용한다. 각 줄은 **필드이름: 값**으로
이뤄지고, 값이 두 줄 이상이면 들여쓰기한다.
```
Description: The description of a package is usually long,
    spanning multiple lines. The second and subsequent lines
    should be indented, usually with four spaces.
```

본 챕터에서는 주요 필드 몇 가지를 소개하려 한다.

### Dependencies: What does your package need?

### Title and description: What does your package do?

### Author: who are you?

### License: Who can use your package?

### Version

### Other components

## Object documentation (`man/`)

> Documentation is one of the most important aspects of a good package.

문서화(documentation)를 잘 해두면 나와 다른 사람 모두에게 도움이 된다. 여러 양식의 문서화 방법이 있는데, 본 챕터에서는 `?`나
`help()`로 열어볼 수 있는 **orient documentation**에 대해 설명하려 한다.

Orient documentation은 **사전과 비슷**하다. 내가 찾아야 하는 검색어가 무엇인지 알 때는 유용하지만, 반대로 해결해야 할
문제만 알고 이를 위해 어떤 검색어가 필요한지 모를 때는 불편할 수 있다. 이런 경우에는 **vignettes**를 사용하게 된다(다음 챕터).

R에서 object documentation하는 방법은 `man/` 폴더에 `.Rd` 파일을 작성하는 것이다. LaTeX 등으로 작성한 후
HTML, 텍스트, pdf 등으로 변환된다. 이를 직접 하는 것보다는, roxygen2 패키지를 사용하는 것이 훨씬 좋다. 뿐만 아니라
roxygen2로 `DESCRIPTION` 파일의 `NAMESPACE` 필드와 `Collate` 필드도 관리할 수 있다. 본 챕터에서는
`.Rd` 파일과 `Collate` 필드에 대해 다룰 것이고, 나머지는
[NAMESPACE](http://r-pkgs.had.co.nz/namespace.html#namespace) 챕터에서 다룰 예정이다.

### The documentation workflow

4단계 절차가 있다.

  1. `.R` 파일에 oxygen 코멘트 추가하기
  2. `devtools::document()` 실행(또는 RStudio에서 `Ctrl/Cmd` + `Shift` + `D`)

    * oxygen 코멘트를 `.Rd` 파일로 변환한다(`devtools::document()`가 `roxygen2::roxygenise()`를 실행함)
  3. `?`로 미리보기
  4. 다듬기

oxygen 코멘트는 `#'`으로 시작한다(작은따옴표가 추가된다).
```
#' Add together two numbers.
#' 
#' @param x A number.
#' @param y A number.
#' @return The sum of \code{x} and \code{y}.
#' @examples
#' add(1, 1)
#' add(10, 1)
add <- function(x, y) {
  x + y
}
```

`Ctrl/Cmd` + `Shift` + `D`를 누르거나 `devtools::document()`를 실행하면 아래와 같은 `man/add.Rd`가 생성된다:

```
% Generated by roxygen2 (4.0.0): do not edit by hand
\name{add}
\alias{add}
\title{Add together two numbers}
\usage{
add(x, y)
}
\arguments{
  \item{x}{A number}

  \item{y}{A number}
}
\value{
The sum of \code{x} and \code{y}
}
\description{
Add together two numbers
}
\examples{
add(1, 1)
add(10, 1)
}
```

첫 번째 줄의 "%~~"는 roxygen2 생성한 파일이고 **수정하면 안 된다.** 보통 `add.Rd` 파일을 들여다 볼 일은 없을 것이다.
[R extensions 메뉴얼](http://cran.r-project.org/doc/manuals/R-exts.html#Rd-format)에
더 자세한 정보가 나와있다.

`?add`나 `help("add")`나 `example("add")`를 실행하면 R은 `\alias{"add"}`가 들어있는 `.Rd` 파일을
찾아서 파싱한다. 결과는 아래와 같다.

![](http://r-pkgs.had.co.nz/screenshots/man-add.png)

문서를 미리 보는 게 가능하다. 만약 미리보기가 되지 않는다면 devtools를 사용하고 있는지, `devtools::load_all()`를
실행헀는지 확인하자.

### Alternative documentation workflow

object documentation은 **빠르지만, 문서에 링크를 포함할 수 없다.** 만약 링크를 포함하고 싶다면 이 챕터에서 소개하는
방법을 사용해보자.

1. `.R` 파일에 roxygen 코멘트 추가하기
2. ![](http://r-pkgs.had.co.nz/screenshots/build-reload.png) 버튼을 클릭하거나
`Ctrl/Cmd` + `Shift` + `B` 누르기.
    * 패키지가 다시 빌드된다(문서 수정사항 반영, 라이브러리에 설치, R 재시작, 패키지 로드)
    * 느리지만 확실한 방법
3. `?`로 미리보기
4. 다듬기

위 방법을 실행하기 전에 아래 옵션을 확인해볼 것!

![](http://r-pkgs.had.co.nz/screenshots/build-reload-opts-2.png)

### Roxygen comments

> Roxygen comments start with #' and come before a function.

함수 앞에 위치한 roxygen 구문을 하나의 **블록(block)**이라 한다. 블록은 `@tagName details`와 같은 형식의
**태그(tag)**로 이뤄진다. 태그에서 `@`를 사용하고 싶으면 `@@`를 입력해야 한다(`@`는 다른 의미가 있음). 각 블록은 첫 태그가
등장하기 전에에 `introduction`이라는 내용으로 시작한다.

* (필수) **첫 문장**은 그 문서의 제목이 된다. `help(package = mypackage)`를 실행했을 때 가장 위에 오는
그것이다.
* (필수) **두 번째 문단**은 설명문이다: 문서에서 제목 바로 다음에 등장하며 그 함수가 무엇을 하는지 설명한다.
* (선택) **세 번째 문단 이후**는 세부 내용이다.

예시:

```
#' Sum of vector elements.
#' 
#' \code{sum} returns the sum of all the values present in its arguments.
#' 
#' This is a generic function: methods can be defined for it directly or via the
#' \code{\link{Summary}} group generic. For this to work properly, the arguments
#' \code{...} should be unnamed, and dispatch is on the first argument.
sum <- function(..., na.rm = TRUE) {}
```

`\code{}`와 `\link{}`는 포맷명령어다([formatting](http://r-pkgs.had.co.nz/man.html#text-formatting) 참고).
문서 한 줄을 80단어 이내로 하기를 추천한다.
**RStudio에서 `Ctrl/Cmd` + `Shift` + `/` 또는 code - re-flow comment 클릭.**

`@section`을 이용해 원하는 제목의 섹션을 추가할 수 있다. 세부 내용을 나눌 때 유용하다. **콜론으로 끝나야 하고, 제목은 한 줄로
작성해야 한다.**

```
#' @section Warning:
#' Do not operate heavy machinery within 8 hours of using this function.
```

`@seealso`와 `@family`도 유용한 명령어다.

```
#' @family aggregate functions
#' @seealso \code{\link{prod}} for products, \code{\link{cumsum}} for cumulative
#'   sums, and \code{\link{colSums}}/\code{\link{rowSums}} marginal sums over
#'   high-dimensional arrays.
```

다른 유용한 명령어로 `@aliases alias1 alias2 ...`와 `@keywords keyword1 keyword2 ...`가 있다.

### Documenting functions

패키지는 함수를 많이 다룬다. 함수를 다룰 때 유용한 세 가지 명령어가 있다.

* `@param name description`: 함수의 입력 자료나 입력 변수의 형식, 하는 일 등을 간결하게 기술한다.
`description`은 모두 대문자로 시작해야 하고, 여러 줄이 될 수 있다. 모든 parameter에 대해 `@param`을 작성해야
한다.
* `@param x,y Numeric vectors..` 등으로 여러 변수를 한 번에 설명할 수 있다(콤마 뒤에 공백 없음!).
* `@examples`는 정상 작동하는 예제 코드를 담아야 한다(`R CMD check`에서 확인).
* `\dontrun{}`를 사용해 에러가 나는 코드를 설명 목적으로 포함시킬 수 있다.
* `@example path/relative/to/package/root`를 이용해 외부 문서에 예제 코드를 인용할 수 있다(example에 s가 없다!).
* `@return description`로 함수가 무엇을 반환하는지 설명한다.

```
#' Sum of vector elements.
#'
#' \code{sum} returns the sum of all the values present in its arguments.
#'
#' This is a generic function: methods can be defined for it directly
#' or via the \code{\link{Summary}} group generic. For this to work properly,
#' the arguments \code{...} should be unnamed, and dispatch is on the
#' first argument.
#'
#' @param ... Numeric, complex, or logical vectors.
#' @param na.rm A logical scalar. Should missing values (including NaN)
#'   be removed?
#' @return If all inputs are integer and logical, then the output
#'   will be an integer. If integer overflow
#'   \url{http://en.wikipedia.org/wiki/Integer_overflow} occurs, the output
#'   will be NA with a warning. Otherwise it will be a length-one numeric or
#'   complex vector.
#'
#'   Zero-length vectors have sum 0 by definition. See
#'   \url{http://en.wikipedia.org/wiki/Empty_sum} for more details.
#' @examples
#' sum(1:10)
#' sum(1:5, 6:10)
#' sum(F, F, F, T, T)
#'
#' sum(.Machine$integer.max, 1L)
#' sum(.Machine$integer.max, 1)
#'
#' \dontrun{
#' sum("a")
#' }
sum <- function(..., na.rm = TRUE) {}
```

### Documenting datasets

### Documenting packages

### Documenting classes, generics and methods

### Special characters

아래 특수문자는 사용에 주의해야 한다.

* `@`: roxygen 태그 시작할 때 사용된다. `@@` 사용해 입력.
* `%`: latex 코멘트 시작할 때 사용한다. `\%` 사용해 입력(example에서는 \ 필요 없다).
* `\`: latex escaping에 사용된다. `\\` 사용해 입력.

### Do repeat yourself

다른 문서에서 설명한 내용을 반복하고 싶지 않을 때 아래 명령어를 사용할 수 있다.

* `@inheritParams`
* `@describeIn` 또는 `@rdname`

### Text formatting reference sheet

roxygen 태그에서는 `Rd` 문법을 사용한다. 아래에서 몇 가지 유용한 활용법을 소개한다. 더 자세한 내용은 [R
extensions](http://cran.r-project.org/doc/manuals/R-exts.html#Marking-text)를
참고하자.

#### Character formatting

#### Links

#### Lists

#### Mathematics

#### Tables

## Vignettes (`vignettes/`): long-form documentation

> A vignette should divide functions into useful categories, and demonstrate how
to coordinate multiple functions to solve problems.

orient documentation이 필요한 키워드(i.e. 함수 이름)를 알 때 유용하다면, vignette는 해결하려는 문제를 알 때
유용하다. 또한, vignette을 통해 패키지 설명을 더욱 자세히 기술할 수 있다.

`browseVignettes()` 명령어로 현재 설치된 모든 vignettes를 볼 수 있다.
특정 패키지의 것만 보고 싶다면 `browseVignettes("packagename")` 명령어를 사용한다.
모든 vignettes는 <u>소스코드, HTML(또는 PDF), R 코드</u> 세 가지를 가지고 있다. 특정 vignette은
`vignette(x)` 명령어로 읽고, `edit(vignette(x))`로 편집할 수 있다.
설치하지 않은 vignette을 읽는 방법은 [여기](CRAN page, e.g., http://cran.r-project.org/web/packages/dplyr)를 참고하자.

R 3.0.0 이전에는 vignette를 만드는 방법이 Sweave 뿐이었다. Sweave는 무겁고 배우기 어려웠다(LaTeX).
하지만 knitr이 개발되고나서는 vignette를 만드는 게 쉬워졌고 거의 모든 패키지에서 vignette를 사용하게 됐다.
이 챕터에서는 <u>knitr의 vignette engine</u>에 대해 설명하려 한다. 이 엔진의 장점을 조금 소개하면 아래와 같다.

* 마크다운 문법을 사용한다. LaTeX보다는 문법이 자유롭지 못 하지만, 대신 문법을 지킨다면 내용에 집중할 수 있다.
* 텍스트, 코드, 결과를 함께 기록할 수 있다.
* rmarkdown 패키지를 사용할 수 있다.

RStudio를 설치할 때 R Markdown 문서를 만드는 데 필요한 모든 것이 자동으로 설치된다.

### Vignette workflow

`devtools::use_vignette("my-vignette")`를 실행하면

1. `vignettes/` 폴더가 생성되고
2. `DESCRIPTION` 내용을 수정하고(i.e. `Suggests`와 `VignetteBuilder` 필드에 knitr 추가)
3. vignette의 초안이 생성된다(`vignettes/my-vignette.Rmd`).

다음으로 할 일은

1. 초안 수정
2. vignette 생성: `Ctrl/Cmd` + `Shift` + `K`
(또는 ![](http://r-pkgs.had.co.nz/screenshots/knit.png) 클릭)

이다.
Vignette에는 **세 가지 중요 구성 요소**가 있다.

* The initial metadata block
* Markdown for formatting text
* Knitr for intermingling text, code and results.

다음 세 섹션에서 각각을 설명하겠다.

### Metadata

메타데이타의 기본 템플릿.

```
---
title: "Vignette Title"
author: "Vignette Author"
date: "`r Sys.Date()`"
output: rmarkdown::html_vignette
vignette: >
  %\VignetteIndexEntry{Vignette Title}
  %\VignetteEngine{knitr::rmarkdown}
  \usepackage[utf8]{inputenc}
---
```

yaml 문법이라서 `DESCRIPTION`과 유사하다. 특별함 점은 `>`를 사용하여 다음에 올 줄이 plain text라는 것을 명시한다는
것이다. 아래는 각 필드에 대한 설명이다.

* Title, author and date
* Output
* Vignette

### Markdown

Vignette 작성할 때는 **마크다운** 문법을 사용한다.

### Knitr

> Knitr takes R code, runs it, captures the output, and translates it into
formatted Markdown.

```
\```{r}
# Add two numbers together
add <- function(a, b) a + b
add(10, 20)
\```
```

를 이용해

```
\```r
# Add two numbers together
add <- function(a, b) a + b
add(10, 20)
## [1] 30
\```
```

와 같은 마크다운으로 바꾸고 렌더링하여

```
# Add two numbers together
add <- function(a, b) a + b
add(10, 20)
## 30
```

를 얻는다.


### Development cycle

`Cmd` + `Alt` + `C`로 각 코드 청크를 실행하고, `Ctrl/Cmd` + `Shift` + `K`로 전체 문서를 실행한다.

`devtools::build()`를 사용해서 패키지와 vignette을 함께 빌드하는 게 좋다.

    * `devtools::build_vignettes()`는 사용하지 말자
    * `build_vignettes = TRUE` 옵션 사용

비슷하게, `devtools::install_github(build_vignettes = TRUE)` 등으로 활용하자.

### Advice for writing vignettes

직접 사람을 가르치면서 작성해보자.
vignette를 작성할 때는 초보자의 입장에서 생각해야 하는데, 패키지를 작성하는 사람에게는 쉽지 않은 일이다.
직접 초보자를 가르치다보면 그들이 무엇을 모르는지, 어떻게 설명해야 할지 배울 수 있다.

그러다보면 내가 코딩하면서 놓친 부분을 발견하고 개선할 수도 있다.

* [Creating passionate users](http://headrush.typepad.com/),
[Serious Pony](http://seriouspony.com/blog/) 추천: 프로그래밍, 가르치기 팁
* [http://amzn.com/0321898680](http://amzn.com/0321898680) 추천: 글쓰기 팁
* 코딩하다가 지쳤을 때 글을 써보자: 글쓰기와 코딩하기는 서로 다른 뇌를 사용한다([structured
procrastination](http://www.structuredprocrastination.com/))

### CRAN notes

> any packages used by the vignette must be declared in the `DESCRIPTION`

* CRAN은 제출된 패키지의 R 코드가 정상 작동하는지 여부를 확인한다.
* 패키지 설치 후에도 vignette가 안 보일 수 있다
    * 폴더 이름을 `vignettes/`가 아니라 `vignette/`로 하면 안 나온다.
    * `.Rbuildignore`에 vignette가 들어있을 수 있다.
    * 메타데이터가 누락됐을 수 있다.
* `error = TRUE`로 설정했다면 `purl = FALSE`도 설정해야 한다.
* 용량에 관한 규칙은 없지만 파일 크기는 최대한 줄이자(그림이 많은 경우 등)

### Where next

* Rmarkdown 문법 공부
* vignette을 <u>Journal of Statistical Software</u>, <u>The R Journal</u> 등에 투고

## Testing (`Tests/`)

> The problem with this approach is that when you come back to this code in 3
months time to add a new feature, you’ve probably forgotten some of the informal
tests you ran the first time around.

함수를 짜고 `devtools::load_all()`로 불러들여서 콘솔에서 실행해보고 다듬기를 반복...

위와 같이 수동으로 코드 테스트를 진행해도 그 당시에는 문제가 없다.
하지만 시간이 지나고 다시 같은 코드를 봤을 때도 자신이 어떤 테스트를 진행했었는지 기억하는 것은 
어려운 일기 떄문에 **과거에 진행해던 테스트를 반복하기 쉽다**.

`testthat` 패키지를 사용하면 코드 테스트를 자동화하고 결과를 저장할 수 있다.
덕분에 나중에도 같은 테스트를 쉽게 반복할 수 있다.

### Test workflow

`devtools::use_testthat()`을 실행하면,

1. `tests/testthat` 폴더가 생성되고
2. `DESCRIPTION` 파일의 `Suggests` 필드에 testthat이 추가되고
3. `tests/testthat.R`이 생성된다. 이 파일이 `R CMD check` 명령을 내렸을 때 모든 테스트를 자동으로 진행해준다.
    * [automated checking](http://r-pkgs.had.co.nz/check.html#check) 참고

그 다음 진행 방법은 간단하다.

1. 코드나 테스트 수정
2. 패키지 테스트 실행: `Ctrl/Cmd` + `Shift` + `T` 또는 `devtools::test()`
3. 1-2 반복

테스트 결과는 아래와 같이 나타난다

```
Expectation : ...........
rv : ...
Variance : ....123.45.
```

각 줄은 테스트 파일 하나를, 각 `.`은 통과한 테스트를, 각 숫자는 통과하지 못한 테스트를 나타낸다.
각 숫자의 세부 내용을 살펴볼 수 있다.

```
1. Failure(@test-variance.R#22): Variance correct for discrete uniform rvs -----
VAR(dunif(0, 10)) not equal to var_dunif(0, 10)
Mean relative difference: 3

2. Failure(@test-variance.R#23): Variance correct for discrete uniform rvs -----
VAR(dunif(0, 100)) not equal to var_dunif(0, 100)
Mean relative difference: 3.882353
```

테스트 내용 (e.g., “Variance correct for discrete uniform rvs”), 위치(e.g.,
“@test-variance.R#22”), 실패한 이유(e.g., “VAR(dunif(0, 10)) not equal to
var_dunif(0, 10)”)를 나타낸다. 목표는 모든 테스트를 통과하는 것이다.

### Test structure

테스트 파일은 `tests/testthat/`에 저장돼있다. 각 이름은 반드시 `test`로 시작해야 한다.
다음은 stringr 패키지의 테스트파일 예시다.

```
context("String length")
library(stringr)

test_that("str_length is number of characters", {
  expect_equal(str_length("a"), 1)
  expect_equal(str_length("ab"), 2)
  expect_equal(str_length("abc"), 3)
})

test_that("str_length of factor is length of level", {
  expect_equal(str_length(factor("a")), 1)
  expect_equal(str_length(factor("ab")), 2)
  expect_equal(str_length(factor("abc")), 3)
})

test_that("str_length of missing is missing", {
  expect_equal(str_length(NA), NA_integer_)
  expect_equal(str_length(c(NA, 1)), c(NA, 1))
  expect_equal(str_length("NA"), 2)
})
```

테스트는 **files**-**tests**-**expectations**로 이어지는(상위->하위) 계층 구조를 가지고 있다. 

* **expectation**: 테스트의 최소 단위. 이름이 `expect_`로 시작하는 **함수**이다.
해당 코드가 예상하는 대로 작동하는지(결과 값, 변수 종류, 에러 여부 및 내용 등) 확인한다.
* **test**: `test_that()`으로 수행한다. 여러 **expectations**로 이뤄지며, 하나의 기능(functionality)을
테스트한다(그래서 **unit**이라고도 불린다). 여러 함수가 관여할 수도 있다.
* **file**: 여러 **tests**의 묶음이다. `context()`에 **human-readable한 이름**을 표기한다. 

#### Expectations

테스트의 최소 단위이다. 테스트 결과가 **예상과 같은지 다른지** 결과를 알려준다.
모든 expectations는 비슷한 구조를 가지고 있다.

* `expect_`로 시작
* 매개변수 두 개: 첫 번째는 실제 결과, 두 번째는 예상 결과
* 두 결과가 다르면 에러 발생

expectations는 tests와 files 안에 들어있지만, **각 expectation을 직접 실행할 수도 있다.**
testthat 패키지에는 약 20 종류의 expectations가 있다.

* test for equality: `expect_equal()`, `expect_identical()`.
`expect_equal()`는 `all.equal()`를 이용해 **설정한 정밀도(숫자) 내에서** 두 결과가 같은지 확인한다.

  ```
  expect_equal(10, 10)
  expect_equal(10, 10 + 1e-7)
  expect_equal(10, 11)
  ```

  완전히 일치하는지를 알고 싶다면 `expect_identical()`를 사용한다(`identical()` 기반).
  
  ```
  expect_equal(10, 10 + 1e-7)
  expect_identical(10, 10 + 1e-7)
  ```
  
* 문자: `expect_match()`. 문자 벡터와 정규표현식을 비교한다. 
`grepl()` 기반이며, `all`을 이용해 모든 문자가 일치해야 하는지 혹은 하나의 문자만 일치해도 되는지 설정할 수 있다.

  ```
  string <- "Testing is fun!"

  expect_match(string, "Testing") 

  # Fails, match is case-sensitive
  expect_match(string, "testing")

  # Additional arguments are passed to grepl:
  expect_match(string, "testing", ignore.case = TRUE)
  ```
  
* `expect_match()`의 4가지 변형: `expect_output()`은 프린트한 결과 비교, `expect_message()`는 메세지 비교,
`expect_warning()`는 경고문 비교, `expect_error()`는 에러 비교.

  ```
  a <- list(1:10, letters)

  expect_output(str(a), "List of 2")
  expect_output(str(a), "int [1:10]", fixed = TRUE)

  expect_message(library(mgcv), "This is mgcv")
  ```

  `expect_message()`, `expect_warning()`, `expect_error()`에서
  매개변수를 하나만 입력하면 메세지(경고, 에러)가 생성되는지 여부를 파악할 수 있다.
  
* `expect_is()`: 객체가 해당 클래스로부터 유래되었는지(inherit) 검사한다.

  ```
  model <- lm(mpg ~ wt, data = mtcars)
  expect_is(model, "lm")
  expect_is(model, "glm")
  ```
  
* `expect_true()`와 `expect_false()`: 다른 expectations가 모두 내 목적에 적당하지 않을 때 유용하다.
*  `expect_equal_to_reference()`: 첫 수행 결과와 다른지 비교.

### Writing tests

test는 테스트 이름과(Test that으로 시작하는 문장) 코드 블럭(expectations)으로 구성된다.
test를 어떻게 구성하는지는 자유지만, **작은 tests 여러 개**가 큰 tests 몇 개보다 나을 때가 많다.

testthat은 R 환경을 다시 원래대로 복구해주지 않는다.

* filesystem: 폴더 생성/삭제/수정 ...
* search path: `library()`, `attach()`
* global options: `options()`, `par()`

따라서, 위 내용이 내 패키지에 들어있다면 직접 원상복구 해줘야 한다(regular R functions 이용).

#### What to test

* internal보다 external interface(??)에 집중하기
* 한 테스트에는 하나의 동작만 포함하기
* 결과가 확실한 코드에 시간낭비 말기
* 버그 발견할 때마다 테스트하기

#### Skipping a test

가끔은 테스트 진행이 불가능할 때가 있다(인터넷 문제 등).
`skip()` 함수로 테스트를 생략할 수 있다. 에러 대신 `S`가 표출된다.

```
check_api <- function() {
  if (not_working()) {
    skip("API not available")
  }
}

test_that("foo api returns bar when given baz", {
  check_api()
  ...
})
```

#### Building your own testing tools

**중복되는 코드를 새로운 함수로 만들어 간소화할 수 있다.**

```
library(lubridate)

## 
## Attaching package: 'lubridate'

## The following object is masked from 'package:base':
## 
##     date

test_that("floor_date works for different units", {
  base <- as.POSIXct("2009-08-03 12:01:59.23", tz = "UTC")

  expect_equal(floor_date(base, "second"), 
    as.POSIXct("2009-08-03 12:01:59", tz = "UTC"))
  expect_equal(floor_date(base, "minute"), 
    as.POSIXct("2009-08-03 12:01:00", tz = "UTC"))
  expect_equal(floor_date(base, "hour"),   
    as.POSIXct("2009-08-03 12:00:00", tz = "UTC"))
  expect_equal(floor_date(base, "day"),    
    as.POSIXct("2009-08-03 00:00:00", tz = "UTC"))
  expect_equal(floor_date(base, "week"),   
    as.POSIXct("2009-08-02 00:00:00", tz = "UTC"))
  expect_equal(floor_date(base, "month"),  
    as.POSIXct("2009-08-01 00:00:00", tz = "UTC"))
  expect_equal(floor_date(base, "year"),   
    as.POSIXct("2009-01-01 00:00:00", tz = "UTC"))
})
```

두 개의 helper functions를 만들어서 더 간단하게 줄일 수 있다.

```
test_that("floor_date works for different units", {
  base <- as.POSIXct("2009-08-03 12:01:59.23", tz = "UTC")
  floor_base <- function(unit) floor_date(base, unit)
  as_time <- function(x) as.POSIXct(x, tz = "UTC")

  expect_equal(floor_base("second"), as_time("2009-08-03 12:01:59"))
  expect_equal(floor_base("minute"), as_time("2009-08-03 12:01:00"))
  expect_equal(floor_base("hour"),   as_time("2009-08-03 12:00:00"))
  expect_equal(floor_base("day"),    as_time("2009-08-03 00:00:00"))
  expect_equal(floor_base("week"),   as_time("2009-08-02 00:00:00"))
  expect_equal(floor_base("month"),  as_time("2009-08-01 00:00:00"))
  expect_equal(floor_base("year"),   as_time("2009-01-01 00:00:00"))
})
```

expectation 함수를 새로 만들어서 더 간소화할 수 있다.

```
base <- as.POSIXct("2009-08-03 12:01:59.23", tz = "UTC")

expect_floor_equal <- function(unit, time) {
  expect_equal(floor_date(base, unit), as.POSIXct(time, tz = "UTC"))
}
expect_floor_equal("year", "2009-01-01 00:00:00")
```

이렇게 하면 마지막 줄이 informative output을 안 줄 수 있다(????).
이럴 때는 [non-standard evaluation](http://adv-r.had.co.nz/Computing-on-the-language.html)를 사용해보자.
`bquote()`와 `eval()`이 핵심인데, 아래 `bquote()`에서  `.(x)`는 `x`를 해당 호출 위치에 놓는 역할을 한다.

```
expect_floor_equal <- function(unit, time) {
  as_time <- function(x) as.POSIXct(x, tz = "UTC")
  eval(bquote(expect_equal(floor_date(base, .(unit)), as_time(.(time)))))
}
expect_floor_equal("year", "2008-01-01 00:00:00")
```

이를 사용해 최종적으로 아래와 같이 간소화 했다.

```
test_that("floor_date works for different units", {
  as_time <- function(x) as.POSIXct(x, tz = "UTC")
  expect_floor_equal <- function(unit, time) {
    eval(bquote(expect_equal(floor_date(base, .(unit)), as_time(.(time)))))
  }

  base <- as_time("2009-08-03 12:01:59.23")
  expect_floor_equal("second", "2009-08-03 12:01:59")
  expect_floor_equal("minute", "2009-08-03 12:01:00")
  expect_floor_equal("hour",   "2009-08-03 12:00:00")
  expect_floor_equal("day",    "2009-08-03 00:00:00")
  expect_floor_equal("week",   "2009-08-02 00:00:00")
  expect_floor_equal("month",  "2009-08-01 00:00:00")
  expect_floor_equal("year",   "2009-01-01 00:00:00")
})
```

### Test files

`파일(file)`은 테스트의 가장 큰 단위이다. 모든 `파일`은 `context()`를 가지고 있다(내용 설명).

`파일` 구성하는 것 또한 만드는 사람 마음이다.
하지만 모든 테스트를 하나의 파일에 놓는 것, 모든 테스트마다 파일을 만드는 것은 피하자.
하나의 복잡한 기능, 함수를 하나의 파일로 만드는 게 좋을 것이다.

### CRAN notes

* 구동 시간이 짧아야 한다(1분 이내): 오래 걸리는 부분은 머리에 `skip_on_cran()`를 써두자.
* 모든 CRAN 테스트는 영어로(`LANGUAGE=EN`), C sort order(`LC_COLLATE=C`)로 진행된다.
* OS마다 다를 수 있는 구문에 주의하자.
예를 들어, 소수점 반올림 문제는 OS마다 다를 수 있으니
`expect_identical()`보다는 `expect_equal()`를 사용하자.

## Namespaces (`NAMESPACE`)

네임스페이스(namespace)는 다른 사람과 내 패키지를 공유하려 할 때 중요한 개념이다(나만 보려고 한다면 중요하지 않을 수 있다).
네임스페이스를 잘 정의하면 내 패키지는 하나의 독립적인 것으로 존재할 수 있게 된다.
따라서 다른 패키지 코드에 영향을 받지 않고 패키지가 구동되는 환경에 덜 구애받게 된다.

### Motivation

네임스페이스는 이름이 중복되는 경우 나타나는 문제를 방지할 수 있다.
특정 패키지의 함수를 지정할 때 사용하는 `::` 연산자도 네임스페이스의 일종이다.
만약 `dplyr`를 로드한 후 이어서 `Hmisc`를 로드했다고 하자. 두 패키지 모두 `summarize()` 함수를 가지고 있는데,
그냥 함수 이름만 호출하면 나중에 로드한 `Hmisc`의 `summarize()`가 호출된다.

네임스페이스는 **import**와 **export** 두 방면에서 패키지를 하나의 독립체로 만들어준다.

**Import**는 패키지 안의 함수 하나가 다른 함수를 어떻게 찾는지를 결정한다. 예를 들어보자.
만약 `nrow()`의 정의를 임의로 바꾸면 어떻게 될까?

```
nrow

## function (x) 
## dim(x)[1L]
## <bytecode: 0x244d5b0>
## <environment: namespace:base>
```

`nrow()` 정의에는 `dim()`이 사용된다. `dim()`의 정의를 아래와 같이 바꾸면 `nrow()`는 어떻게 될까?

```
dim <- function(x) c(1, 1)

dim(mtcars)
## [1] 1 1

nrow(mtcars)
## [1] 32
```

놀랍게도 `nrow()`는 변하지 않는다. `dim()`을 찾을 때 패키지 네임스페이스를 이용하기 때문이다.
우리가 정의한 <u>global environment에 있는 `dim()`</u>이 아닌
<u>base environment에 있는 `dim()`</u>을 참고한다는 뜻이다.

**Export**는 패키지의 함수 중 어떤 것들이 외부 패키지가 사용할 수 있는지 지정해준다.
이렇게 해서 다른 패키지와의 충돌을 막아준다.

### Search path

네임스페이스가 왜 중요한지 이해하기 위해서는 search path를 이해할 필요가 있다.

R이 함수를 호출하려면 그것을 찾아내야 한다.
가장 먼저 찾아보는 곳은 global environment이고 여기에 없으면 search path를 찾아본다.
search path에는 내가 **attach**한 패키지 리스트가 담겨있다. `search()` 명령어로 확인할 수 있다.

```
search()

##  [1] ".GlobalEnv"          "package:oldbookdown" "package:rmarkdown"  
##  [4] "package:stats"       "package:graphics"    "package:grDevices"  
##  [7] "package:utils"       "package:datasets"    "package:methods"    
## [10] "Autoloads"           "package:base"
```

패키지를 loading하는 것과 attaching하는 것은 다르다.
보통 `library()`가 loading하는 것이라 생각하기 쉽지만, 사실 이는 attaching하는 것이다.

패키지가 설치된(installed) 경우

* **Loading**은 1) 코드, 데이터, DLL 파일을 로드하고 2) S3, S4 메서드를 등록하고(register) 3) .onLoad() 함수를 실행한다.
로딩이 끝나면 패키지를 메모리에서 사용할 수 있게 된다. 하지만 아직 search path에는 없기 때문에에 `::`를 사용해서 접근해야 한다.
사실 `::`역시 패키지를 로드한다(안 돼있을 경우).
패키지를 직접 로드하는 경우는 별로 없지만, 가능은 하다(`requireNamespace()`나 `loadNamespace()`)
* **attaching**은 <u>로딩한</u> 패키지를 search path에 등록한다.
즉, `library()`와 `require()`은 loading과 attaching을 모두 수행하는 함수인 것이다.

패키지가 설치되지 않았다면 loading(attaching도)할 수 없다(에러 발생).

예를 들어 `expect_that()`를 사용한다고 하자.
`library()`를 사용하면 testthat이 search path에 등록되겠지만, `::`의 경우는 그렇지 않다.

```
old <- search()
testthat::expect_equal(1, 1)
setdiff(search(), old)

## character(0)

expect_true(TRUE)

## Error in expect_true(TRUE): could not find function "expect_true"

library(testthat)
expect_equal(1, 1)
setdiff(search(), old)

## [1] "package:testthat"

expect_true(TRUE)
```

패키지를 사용하는 방법은 네 가지가 있다. loading/attaching 여부, 에러 발생 여부로 구분할 수 있다.

|       | **Throws error**   | **Returns** `FALSE`                   |
|:------|:-------------------|:--------------------------------------|
| Load  | loadNamespace("x") | requireNamespace("x", quietly = TRUE) |
| Attach| library(x)         | require(x, quietly = TRUE)            |

위 네 가지 중 두 가지만 사용해야 한다.

* `library(x)`: 일반 R 스크립트에서 사용한다. 패키지에서는 절대 사용하지 않는다.
* `requireNamespace(x, quietly = TRUE)`: 패키지 안에서 사용한다.

`require()`(대부분 requireNamespace()가 더 좋다)이나 `loadNamespace()`는 사용할 필요가 없다.
`require()`나 `library()` 대신 `DESCRIPTION`의 `Depends`와 `Imports` 필드를 사용한다.

그렇다면 `DESCRIPTION`에서 **`Depends`와 `Imports`의 차이**는 무엇일까.

두 필드 모두 필요한 패키지가 미리 설치되어 있도록 해주는 점은 같다.
`Imports`는 패키지를 *load*하고 `Depends`는 *attach*한다는 차이가 있다.

특별한 이유가 없다면 `Imports`를 사용하는 게 좋다.
최대한 global environment를 건드리지 않는 게 좋기 때문이다(search path 포함).
다만, 만약 다른 패키지와 연동해 사용하는 경우는 `Depends`를 사용한다.
예를 들어, analogue 패키지는 vegan 패키지를 기반으로 한다.
vegan이 없는 환경에서는 무용지물이기 때문에 `Depends`를 사용한다.

이제 imports와 exports를 다룰 건데, 이들은 모두 `NAMESPACE`에 기록된다.
먼저 `NAMESPACE`가 어떻게 생겼는지 살펴보자.

### The `NAMESPACE`

다음은 testthat 패키지 `NAMESPACE` 파일의 일부를 발췌한 것이다.

```
# Generated by roxygen2 (4.0.2): do not edit by hand
S3method(as.character,expectation)
S3method(compare,character)
export(auto_test)
export(auto_test_package)
export(colourise)
export(context)
exportClasses(ListReporter)
exportClasses(MinimalReporter)
importFrom(methods,setRefClass)
useDynLib(testthat,duplicate_)
useDynLib(testthat,reassign_function)
```

각 줄은 **directive**(`S3method()`, `export()`, `exportClasses()` 등)를 하나씩 가지고 있다.
각 **directive**는 R 객체 하나가 다른 패키지에서 들여왔는지,
혹은 다른 패키지에서 사용할 수 있도록 export되었는지를 알려준다.

전체 8개의 **directive**가 있다(4개는 exports관련, 4개는 imports 관련)

* `export()`: 함수를 내보낸다(S3, S4 generics 포함).
* `exportPattern()`: 패턴과 일치하는 모든 함수를 내보낸다.
* `exportClasses()`, `exportMethods()`: S4 클래스 및 매서드를 내보낸다.
* `S3method()`: S3 매서드를 내보낸다.

* `import()`: 한 패키지의 모든 함수를 가져온다.
* `importFrom()`: 선택한 함수를 가져온다(S4 generics 포함).
* `importClassesFrom()`, `importMethodsFrom()`: S4 클래스 및 매서드를 가져온다
* `useDynLib()`: C 언어 함수 하나를 가져온다([compiled code](http://r-pkgs.had.co.nz/src.html#src) 참고).

roxygen2를 사용하면 `NAMESPACE` 파일을 쉽게 작성할 수 있다(일일이 쓰지 않아도 된다).
roxygen2를 사용하는 것의 장점은 크게 세 가지가 있다.

* 네임스페이스가 관련 함수 바로 옆에 정의돼 있으므로 import/export 구분이 쉽게 가능하다.
* @export 태그만 사용하면 자동으로 적합한 directive를 생성해준다.
* 간결해진다. 일일히 함수 옆에 directive를 작성해도 roxygen2가 하나로 묶어준다(패키지 작성할 때는 하나하나 적는 게 편하다).

roxygen2가 `NAMESPACE`, `man/*.Rd` 둘 중 하나만, 혹은 둘 다 생성할 수 있게 만들 수 있다.
네임스페이스 관련 태그가 없으면 전자가, documentation 관련 태그가 없으면 후자가 생략된다.

### Workflow

roxygen2로 네임스페이스 생성하는 방법은 function documentation 생성하는 것과 동일하다.
`#'로 시작하는 roxygen2 블록과 태그(@로 시작)를 사용한다. 방식은 다음과 같다.

1. `.R files`에 roxygen 코멘트 추가하기.
2. RStudio에서 `devtools::document()`(또는 `Ctrl/Cmd` + `Shift` + `D`) 실행하기(roxygen 코멘트 -> `.Rd files`).
3. `NAMESPACE` 확인하고 테스트하기.
4. 수정 및 반복하기.

### Exports

Exports하고 싶을 때 읽어보자.

### Imports

Imports하고 싶을 때 읽어보자.

## Data (`data/`)

세 가지 방법으로 패키지에 데이터를 포함시킬 수 있다.

* binary data, 공개: `data/`에 넣기. 예제 데이터셋 넣기 좋다.
* parsed data, 비공개: `R/sysdata.rda`에 넣기. 함수가 작동하는 데 필요한 데이터 넣기 좋다.
* raw data: `inst/extdata`에 넣기.
* 패키지 소스에 포함시키기(직접 생성 또는 `dput()` 이용).

**데이터 넣고 싶을 때 더 읽어보자**

### Exported data
### Internal data
### Raw data
### Other data
### CRAN notes

## Compiled code (`src/`)

**R에서 c, cpp 등 컴파일 언어 사용하는 방법(속도 향상)**

**필요할 때 읽고 정리하자**

## Installed files (`inst/`)

패키지를 설치하면(install) `inst/`에 있는 모든 내용이 복사되어 패키지의 최상위 경로로 이동한다.
이런 점에서 `inst/`와 `.Rbuildignore`는 서로 반대 기능을 한다(복사할 것/안 할 것 지정).
`inst/` 내용을 구성할 때는 **한 가지만 주의**하자.
최상위 폴더에 복사될 것이기 때문에 `inst/`의 내용이 기존 하위 경로의 이름과 중복되서는 안 된다.
즉, `inst/build`, `inst/data`, `inst/demo`, `inst/exec`, `inst/help`, `inst/html`, `inst/inst`,
`inst/libs`, `inst/Meta`, `inst/man`, `inst/po`, `inst/R`, `inst/src`,
`inst/tests`, `inst/tools`, `inst/vignettes`는 사용할 수 없다.

이번 챕터에서는 `inst/`에서 가장 자주 등장하는 파일을 다룰 것이다.

* `inst/AUTHOR`, `inst/COPYRIGHT`: 저작권 관련 내용을 기술한다.
* `inst/CITATION`: 어떻게 인용하는지 기술한다
([package citation](http://r-pkgs.had.co.nz/inst.html#inst-citation) 참고).
* `inst/docs`: 요즘은 잘 쓰지 않는다.
* `inst/extdata`: 데이터셋 설명을 기술한다
([external data](http://r-pkgs.had.co.nz/data.html#data-extdata) 참고).
* `inst/java`, `inst/python` 등: 다른 언어 관련 내용을 기술한다
([other languages](http://r-pkgs.had.co.nz/inst.html#inst-other-langs) 참고).

`inst/`에 있는 파일은 `system.file()`로 찾을 수 있다.
예를 들어 `inst/extdata/mydata.csv`를 찾고 싶다면,
`system.file("extdata", "mydata.csv", package = "mypackage")`를 사용할 수 있다.
함수 안에 `inst/`를 명시하지 않았는데,
패키지가 이미 설치돼 있다면(혹은 `devtools::load_all()`로 로딩된 상태라면) 잘 작동할 것이다.

### Package citation

**인용 형식 작성하는 방법**

### Other languages

**다른 언어 설명 추가하는 방법**

보통 다른 언어 설명은 하지 않지만, 
해당 패키지에서 다른 언어 의 모듈이 큰 부분을 차지한다면 넣어야 한다.
이 때는 `inst/python`과 같이 `inst/` 폴더 안에 추가 경로를 만들어주고,
`DESCRIPTION`의 `SystemRequirements` 필드에도 명시해줘야 한다.
단, Java는 예외이다(`java/` 폴더를 만들고 `.Rinstignore`에 명시해줄 것, `Imports`에 `rJava` 추가할 것).

## Other components

# Best practices
## Git and GitHub

## Checking

## Release

​    

