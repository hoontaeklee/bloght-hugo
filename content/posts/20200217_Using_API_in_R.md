---
title: "R에서 Open API 사용하기 - 카카오 지도"
author: "Hoontaek Lee"
date: 2020-02-17T19:46:25+09:00
publishdate: 2020-01-27 20:33:00+09:00
description:
draft: false
hideToc: false
enableToc: true
enableTocContent: false
tocPosition: outer
tocLevels: ["h2", "h3", "h4"]
tags:
- 2020
- R
series:
-
categories:
- R
image:
---

## Intro

연구실에서 **여러 장소의 주소 --> 경위도 좌표** 변환을 할 일이 있다.

하나하나 웹페이지에서 하기는 많으므로 코딩을 하기로 했다.

API를 사용하면 되는 듯하다.



## API?

Application Programming Interface.

구글에 검색하면 [잘 설명한 글](https://brunch.co.kr/@cysstory/115)을 여럿 찾아 볼 수 있지만, 나름대로 한 번 적어보고 넘어가려 한다.

나는 API를 **술집 종업원**에 비유하려 한다. 술집에서는 여러 **안주요리나 술**을 팔고 있다. 손님들은 술집에 들어가면 **종업원**에게 **신분증**을 보여줘 미성년자가 아님을 확인한다. 그리고 종업원을 통해 술과 먹태를 주문하면, 종업원은 주문 내용을 조리실에 전달해 요리를 손님에게 전달해준다.

우리는 API(점원)를 통해 누군가 잘 만들어 놓은 프로그램(요리, 술)을 쉽게 사용할 수 있다. 단, 그러기 위해서는 나의 **인증키**(신분증)를 보여줘야 하고, API(종업원)를 통해 **일정한 형식**에 맞춰(이거 이거 주세요) 프로그램을 호출(주문)해야 한다.

요즘은 각 술집(네이버, 카카오, 구글, 정부, ...)마다 종업원을 통해 사용할 수 있는 요리(프로그램)를 여럿 마련해놨다. 다만, 어떤 것은 사용 횟수 제한 등의 조건이 있다.

**(내가 이해를 잘못해서 종업원이 여러 요리를 담당하는 게 아니라 실제로는 각 요리마다 담당 종업원이 있는 것일 수 있다)**



## Code Structure

R에서 API를 사용할 때 코드 구조는 

1. 입력사항 준비(검색할 주소 목록, 인증키 등)
2. API 사용
3. 결과 가공

이렇게 된다.

1, 3은 사용자마다 필요한 내용이나 사용하는 라이브러리 등에 따라 매우 다양해진다.

하지만 본 코드의 핵심인 2는 크게 변하지 않을 듯하다.



## Code

```R
##
# 기능
# Open API map (원하는 API 지도로 대체 가능. 여기서는 카카오지도사용)에
# 주소 목록 입력 -> 각 주소의 x, y 좌표 검색 결과 추출
##
# 참고
# 공간통계를 위한 데이터 사이언스 by xwMOOC 4. 다음 지도 API
# (https://statkclee.github.io/spatial/geo-info-lonlat.html#fn5)
##

##
# 1. 입력사항 준비
##

# load libraries
library(httr) # GET()
library(jsonlite) # fromJSON()
library(dplyr)

# 검색할 주소 목록
address_list <- c('서울특별시 송파구 잠실동 40-1',
                  "서울특별시 종로구 사직로 161",
                  "서울특별시 동대문구 청량리동 회기로 57"
                  )

# Web API key
KAKAO_MAP_API_KEY = "My API Key"

# 결과 저장용 데이터프레임
bowl = data.frame()

# 주소별 반복
for(i in 1:length(address_list)){

##
# 2. API 사용
##
    
  # GET함수: GET 프로토콜 형식으로 API 호출
  addr2coord_res <- 
    GET(
      # 카카오 주소검색API
      url = 'https://dapi.kakao.com/v2/local/search/address.json', 
      # 검색어
      query = list(query = address_list[i]),
      # 헤더(API마다 다를 수 있다)
      add_headers(Authorization = paste0("KakaoAK ", KAKAO_MAP_API_KEY)))
  
##
# 3. 결과 가공
##
    
  # KPMG 지리정보 데이터프레임
  kpmg_list <- addr2coord_res %>% 
    content(as = 'text') %>% 
    fromJSON()
  
  # 검색 결과 중 원하는 인자  추출
  row_temp = 
    cbind(
      ## 지명주소
      kpmg_list$documents$address %>% 
        select(address_name),
      
      ## 도로명주소
      kpmg_list$documents$road_address %>% 
        select(address_name, building_name, zone_no, x, y))
  
  # 데이터프레임에 저장
  bowl = rbind(bowl, row_temp)
}
```

1. `KAKAO_MAP_API_KEY`는 필요한 키를 찾아 넣는다(웹인지, 자바스트립튼지...)
2. `GET`함수의 내용은 어떤 API를 사용할 건지(`url`), 어떤 형식으로 결과를 받을 건지(`.json`), 해당 API가 어떤 헤더를 요구하는지(`add_headers`)에 따라 바꿔주면 된다.



## Close

처음으로 R에서 API를 사용해봤다.

생각보다 복잡하지 않았다.

지도 외에도 검색엔진 등 다른 API도 이런 방법으로 적용할 수 있을 것 같은 기분이 든다.