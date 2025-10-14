---
title: "Ecological Forecasting"
author: "Hoontaek Lee"
date: 2020-03-11T20:35:43+09:00
lastmod: 2020-03-11T21:39:43+09:00
description:
cover: 
  relative: true
draft: false
hideToc: false
enableToc: true
enableTocContent: false
tocPosition: outer
tocLevels: ["h1", "h2", "h3"]
tags:
- Book Review
- Research
- 2020
---

<img src="https://image.aladin.co.kr/product/9669/22/cover500/0691160570_2.jpg" style="zoom:100%;" />



# Intro

[Near-term Ecological Forecasting Initiative (NEFI) Summer Course 2020](https://ecoforecast.org). 

책 저자이자 보스턴 대학교(Boston University)에 재직중인 Dietze 교수는 매년 Bayesian application to ecological forecasting을 가르치는 summer course를 진행하고 있다. NEFI 2019에는 선발되지 못했지만, 올해는 고맙게도 나를 초대해줬다.

이 책을 교재로 사용하는데, 가서 잘 배우려면 한 번 예습은 해야 하지 않을까...해서 구입했다.

내 toolbox에 담을 수 있을만한 주제이니 잘 공부해두면 도움이 많이 되겠다. 챕터마다 요약도 잘 돼 있고, [Github](https://github.com/EcoForecast/EF_Activities)에 exercise 코드도 정리돼있고, 중간중간 기억해둘만한 표현도 꽤 있다.

이런 책을 쓸 날이 올까.



## Erratum

- 30 p. 8th line from the below: "<u>we be</u> able to"

# 1. Introduction

## 1.1. Why forecast?

> 기후변화와 더불어 생태계 역시 급격히 변하고 있다. 정책 관련 의사결정을 돕고 생태계 변화 이면을 더 잘 이해하기 위한 도구로서 EF가 필요



Decision making & Understanding ecological processes

- We live in an era of rapid and interacting **changes in the natural world**
- Ecological questions about the future status are being asked by **policymakers**
- How do we, as ecologist, provide the best available **scientific predictions**?
- Quantitative tests are at the heart of the scientific method for advancing our knowledge

<br>

Capture uncertainties

- Coarse understanding, noisy data, and site-specific dynamics defy our understanding
- Ecological forecasts need to capture these uncertainties to be more predictive science



## 1.2. The informatics challenge in forecasting

> EF는 결국 관측 자료를 다루는 일일 것인데, 이는 대부분 생태학자가 미흡한 부분이기에(교육과정) 이 책을 통해 다루려 한다.



- Ecological forecasts may end up being devoted to data management and processing
- The informatics will be leveraged when performing syntheses and making forecasts



## 1.3. The model-data loop

> 데이터로 모델을 맞추고, 
>
> 그렇게 맞춘 모델의 uncertainty 분석을 통해 어떤 데이터가 필요한지 찾고,
>
> 새로 얻은 데이터를 추가해서 새로운 모델을 맞추고
>
> ...



- Forecasting the future status of real systems **requires data** about thos systems
- The model-data loop refers to the idea of **iteratively using data to constrain models and  then using models to determine what new data is most needed**
- The model-data loop applies **regardless of the complexity** of the model



## 1.4. Why Bayes?

> Bayes는 사전확률 설정 -> 데이터 추가 -> 사전확률 조정(=사후확률 계산)의 과정을 거치는데,
>
> 이것이 the model-data loop idea와 흡사하다.



The Bayesian approach

- allows us to treat **all the terms** in a forecast as probability distributions
- is able to **update predictions** as new data becomes available
- tends to be flexible and robust, **allowing us to deal with the complexity of real-world data** and to forecast with relatively complex models.



## 1.5. Models as scaffolds

> 여기저기서 데이터가 쏟아지고 있는데 서로 측정 방법, 측정 스케일, 방법, 가정, 목표하는 process (증발산 vs 증발), 등 같은 분야에서도 서로 다른 점이 너무 많다.
>
> 이 데이터들을 통합하는 데 model이 가교(scaffold) 역할을 할 수 있다.
>
> Model을 이용해 여러 data를 통합하면서 model-data loop idea를 실현 --> models as scaffold approach



Three modeling approaches:

1. Forward modeling: use observed inputs to generate output sets
2. Inverst modeling: use observations of model outputs to infer the most likely inputs
3. Model as scaffold: use models and data together to constrain estimates of different ecosystem variables
   - Different data sets may not be directly comparable to one another (scales, assumptions, target processes, ...), **but may all be comparable to the model**
   - Combining data and models is a fundamentally data-driven exercise



## 1.6. Case studies and decision support

> 연구용 EF와 Decision support는 다른 문제.
>
> Decision support는 
>
> 생태계에 대한 이해가 선행돼야 하고
>
> value, trade-offs 등 가치판단이 추가된다.
>
> 때문에, 책 후반부에 다룰 예정이다.



Prediction vs. Projection

- Prediction: probabilistic forecasts **based on current** trends and conditions
- Projection: probabilistic forecasts driven **by explicit scenarios**



# 2. From models to forecasts

## 2.1. The traditional modeller's toolbox

> 지금까지 뉴턴식 결정론적 사고에 입각한 관점에서 교육을 받아왔다. 
>
> 하지만 이제부터 모든 것을(데이터, 모델) random variable로 간주하고 확률분포를 두는 사고를 해야 한다.
>
> 우리의 지식, 자연의 변화 모두 uncertainties를 포함하고 있기 때문이다.



- The core difference between forecasting and theory ins't a specific set of quantitative skills, but rather in the way we see the world (deterministic and Newtonian way).
- The traditional approach emphasizes *equilibria*, the lack of change in a system over time, and *stability*, the tendency for a system to return to equilibrium when perturbed.
- **Traditional ecological theory does a bad job** of making connections between models and measurements.
- **Modern ecosystems are rarely in equilibrium**, and knowing the current trajectory of a system is often more important to policy and mangement than an asymptotic equilibrium.
- Although stability also has a large impact on how well we can forecast, we require to shift the focus of our modeling **to be less deterministic and to think probabilistically** about both data and models.



## 2.2. Example: The logistic growth model

> 로지스틱 성장 모형이 많이들 익숙할테니, 이걸 예시로 uncertainty 종류를 소개하겠다.



- Logistic growth model: dN/dt = rN(1-N/K)

  where N is the population size, K is the carrying capacity, and a is a constant.



## 2.3. Adding sources of uncertainty

> obervation error
>
> parameter uncertainty
>
> initial condition uncertainty
>
> process variability
>
> others: model selection uncertainty, driver and scenario uncertainty, numerical approximation errorS



- uncertainty: **our ignorance about a process** and should decrease asymptotically with sample size
- variability: **variation in the process itself** that are not captured by a model



### 2.3.1.  Observation error

> 조금이라도 무조건 존재한다.
>
> 모델링하려는 대상 자체에는 영향 없다(광합성 진행과 상관 없이 우리가 측정하면서 만드는 오차).
>
> 결정론적 관점 : residual error = observation error (자연의 상태는 결정돼있으므로 오차x).



- The mean of zero implies that the observations are unbiased
- The key to understanding observation error is to realize that **it does not affect the underlying process itself**.
- Most statistical models **deem residual error as being 100% observation error**
- **Increasing sample size does not reduce it**; It does not disappear asymptotically
- If observation error was the only source of uncertainty, then this forecast would have zero uncertainty because observation error doesn't affect the system itself.



### 2.3.2. Parameter uncertainty

> 모델의 모수 값을 결정할 때 발생하는 오차이다.
>
> 모델링하려는 대상 자체에는 영향 없다.



- is the uncertainty about the true values of all the coefficients in a model
- treats the underlying model as deterministic; just the model calibration arouses errors
- 

Box 2.1. Covariance

**Variance** is a special case of covariance (covariance between a variable and itself).

**Any covariance matrix can be decomposed** into a diagonal matrix of standard deviations for each X and a matrix of correlation coefficients: **DRD**

**independency of the two variables** can be determined by their covariance matrix (independence -> off-diagonal elements will be zero).

Covariances are **critical to the "model as scaffold" idea** where we use correlations among the variables to constrain one variable based on observations of another.

### 2.3.3. Initial conditions

> 초기조건 혹은 state variables는 계의 (변화 방향이 아닌) 현재 상태를 나타내는 값이다.
>
> Equilibria에는 큰 영향이 없지만, 안정상태 도달 전에는 영향이 크다. 
>
> Equilibria를 논하는 theoretical ecology와는 달리 forecasting은 trajectory(어떻게 변화해갈 것인지)를 다루기 때문에 state variables에 관심이 크다.
>
> 모델링하려는 대상 자체에는 영향 없다.



- The initial conditions specify **the starting values of the system's state variables**
  - **state variables** are those that give a snopshot of the system's properties at any single point in time.
  - **variables describing the changes of those states** are typically not treated as state variables
  - (pool sizes, age structure, species composition) vs (recruitment, mortality, NPP)
- In forecasting we are often **much more interested in the current trajectory of a system** than its theoretical asymptote.
- More complex models often have multiple state variables, requiring the estimation of maps of multiple quantities.

Box 2.2. Chaos

**What defines chaotic systems** is their *sensitivity to initial conditions*: A population forecast with slightly perturbed initial condition will have a different trajectory from the original.

**Lyapunov exponent** is a parameter that describes **the rate of change** of the difference between the trajectories and **the different trajectories will diverge or converge**.

**Predictability와 관련된다는 이야기가 나오는데, 잘 모르겠다.**



**An important question** is that how chaotic dynamics impact out ability to make forecasts.

- many of the tools ecologists are using for forecasting are borrowed from atmospheric science, **where the initial condition uncertainty dominates the problems**.
- However, for ecological forecasting, **more important question** is how chaotic dynamics impact our ability to make forecasts.
- **determining what the fundamental nature of the ecological forecasting problem is** will in turn affects the tools we use and how successful we are.

### 2.3.4. Process error

> 모의 대상 자체에서 발생한 모든 uncertainties를 의미한다(모델이 잘못 계산한 것, 모델에 포함하지 못한 process에서 발생한 것 등).
>
> 모의 대상 자체에 영향을 미친다.
>
> 결정론적 관점의 모델에서는 process error도 observation error로 간주한다.



- Process error encompasses all of the sources of true variability in the underlying process that are not captured by the model.

  - Demographic and environmental stochasticity are examples.

    (c.f. **Stochastic models** draw and add random numbers to the dynamics of a model to represent the discrete nature of births and deaths and the unpredictable year-to-year variability of the **climate**)

- Process errors **affet the underlying model dynamics**.

- **Process errors can propagate** forward in time, outward in space, and across any other unit being investigated and **can be partitioned in various ways**, including additive, independent, and autocorrelated ways.



### 2.3.5. Other sources of uncertainty

> 모델 선택에서 발생: 앙상블 사용해서 줄인다.
>
> 입력 자료가 가진 오차: observation error이지만 모델에 사용되는 자료이기 때문에 모델에도 옮겨갈 수 있다.
>
> Numerical approximation errors: 보통은 별로 크지 않지만 상당한 경우도 있다.



- Model choice:
  - increasing the complexity of a model increases parameter error but reduces process error.
  - **There is no guarantee that any of models being considered are correct**.
  - It is generally beneficial to work with **a set of models (ensemble), essentially treating model structure like a discrete random variable**.
- Driver uncertainty or boundary condition uncertainty: Uncertainty in model inputs
- Scenario uncertainty
- Numerical approximation



## 2.4. Thinking probabilistically

> 모든 파라미터를 random variable 취급하고 각각에 적당한 확률분포를 부여한다.
>
> 설령 매커니즘이 확실히 밝혀졌더라도 관측 오차 등을 완전히 없앨 수는 없으므로 이러한 불완전성을 표현한다는 점에서도 적합한 방법이다.



- Everything in the model is described in terms of probability distributions.
- Philosophically, treating parameters as random variables doesn't necessarily mean that the process itself is stochastic. It is a statement about **our imperfect understanding**.



## 2.5. Predictability

> prediction은 원래 어려운 것이다.
>
> 하나의 가설이나 기존의 데이터에만 집착하지 말고, 여러 가설을 비교 검증하고, 새로운 데이터를 적극 활용해야 한다.



- We know there are **known unknowns**, but there are also **unknown unknowns**.
  - known unknowns: we put them using **probabilistic distributions.**
  - unknown unknowns: aka "**black swans**." Failing to anticipate this probability of disturbance does not actually have a huge impact on the mean but results in enormously **overconfident results**.



### 2.5.1. Barriers to forecasting

> 1. 태생적 한계(애초에 예측이 불가능)
> 2. 단순화 불가능한 대상
> 3. 대상에 대한 지식 부족



- inherent barriers: such as local disturbances
- computational irreducibility: cannot use an explicit representation of detailed processes such as species niche spaces. It limits the predictability of important global change processes.
- failures to understand: unlike to weather forecasting models, ecological models cannot represent the physics of the target processes. This may **limit the usability of the pending big ecological data**.



### 2.5.2. Weather forecasting

> 날씨 예측용 모델, 기술이 많이 발달 돼 있음.
>
> 날씨 예측과 생태계 예측 문제의 서로 다른 점을 잘 파악하여(초기 조건 민감성 등) 그들의 toolbox를 잘 활용하자. 
>
> 지금 당장 시작하자. 완벽히 이해하고 시작할 필요 없다. 모델 쓰면서 이해도도 더 높아질 것이다.



- **Ecologists can no longer wait to start making forecasts**, and it is unrealistic to postpone forecasting until we have perfect knowledge.
- The atmosphere is highly chaotic, which makes these models very sensitive to initial conditions.
- It is an open question **how many of these tools can be used as-is by ecologists**.



### 2.5.3. The ecological forecasting problem

> **어렵다.**
>
> Ecological forecasting에서 자주 쓰는 a general form of logistic growth model을 예시로 주고, 
>
> 예측 대상의 uncertainty를 표현한 식에서 각 항의 의미를 자세히 분석하고 있다.
>
> 어떤 적용 사례에 대해서도 uncertainty를 분해해서 각 항별로 정량화 & 중요도 비교가 가능하다!
>
> uncertainty를 잘 파악해야 overconfident를 피할 수 있다.



- There are important differences between the nature of the forecasting problem in meteorology versus ecology.

- Y<sub>t+1</sub> = f(Y<sub>t</sub>, X<sub>t</sub> | theta_bar + alpha) + epsilon

  **Var[Y<sub>t+1</sub>] = (stability x IC uncert) + (driver sens x driver uncert) + {param sens x (param uncert + param variability)} + (process error)**

  - IC tems: 
    - Internal (= endogenous) stability. 
    - Because it is recursive, it **will dominate all other term if |df/dy| > 1**.
    - There are definitely ecological systems that **appear to be chaotic (too sensitive to the IC)**, so my personal working hypothesis is that for most ecological forecasting problems **we need to focus on the other terms**.
    - The only term that shows the **recursive property** (i.e. exponentially increase or decrease), which means **it will increase into the future**.
  - Driver terms:
    - External (= exogenous) sensitivity
    - The magnitude of this term will be problem specific.
    - We might use different covariates for forecasting than we use for explaining the same process.
    - Experimental design for forecasting is often different from that for hypothesis testing.
  - parameter terms:
    - parameter uncertainty (how well do we know the mean of theta?)
    - parameter variability: the variability of the process itself; **another manifestation of the process error**
  - process error
    - errors from processes not explained by the model
    - stochasticity: disturbances, dispersal, mortality, reproduction, ...
    - structural uncertainty: aroused by empirical equations rather than those based on physical laws
    - heterogeneity in space, time, and phylogeny
  - **The power of the equation** is that for any particular application it gives **a quantitative way of breaking down the overall forecast** into its components and **comparing their relative size and importance**.
  - **It is more pressing to quantify variability than it is to explain it.**



# 3. Data. Large and Small



## 3.1. The data cycle and best practices

> 미래의 나를 위해서 + 코웤 증가하는 시대에 맞춰
>
> 데이터를 **잘** 관리해야 한다 - 일정 형식 + 메타데이터

<br>


- Data Life Cycle: two scales
  1. data generation: plan - collect - assure - describe - preserve
  2. synthesis and forecasting: discover, integrate, and analyze
- Best practices
  1. automated
  2. documented
  3. recoverable



### 3.1.1. Plan

> 계획을 잘 짜야 후환이 적다
>
> 어차피 grant proposal에도 써야 한다



### 3.1.2. Collect

> 미리 열제목 등 틀을 만들어 놓자.
>
> 그날 모은 건 그날 확인하자.



### 3.1.3. Assure

> QA/QC 잘 하자. 
>
> 원 값을 바꾸기보다는 QA/QC 플래그를 추가하는 게 좋다.



### 3.1.4. Describe

> 메타데이터 만들자.



### 3.1.5. Preserve

> 변경 기록 잘 하자.
>
> 공개 무료 저장소를 사용하자.



### 3.1.6. Discover, integrate, analyze

> 데이터 다루는 스킬 갖추자.



## 3.2. Data standards and metadata

### 3.2.1. Metadata

> Data's provenance: 메타데이터 잘 쓰자.



### 3.2.2. Data standards

> 정답이 있는 건 아니지만, 그래도 서로 합의 하에 **일정한 형식**으로 데이터를 작성하자.



## 3.3. Handling big data

> Big-data: size, RAM size, handling tool ... 


Box 3.1. Self-documenting Data

The key to the self-documenting data is that the data and the metadata are stored together.

The two most common self-documenting file formats:

- the network common data format (**netCDF**)
- the hierarchical data format (**HDF**)


# 4. Scientific Workflows and the Informatics of Model-Data fusion

## 4.1. Transparency, accountability, and repeatability

> 재현가능해야 한다 --> 데이터, 방법, 소프트웨어 투명하게 공개
>
> 오픈소스 소프트웨어 적극 활용합시다.



## 4.2. Workflows and automation

>재현가능해야 한다 --> 각 과정이 정확히 기록돼야 한다 --> version control (e.g. Git)



- Workflow: A sequence of steps performed in an analysis

Box 4.1. Software Development Tools

An example of software development pattern

1. **세팅**: *pull* the latest code from the mainline repository to your local repository
2. **할 일 체크**: issue tracking system에 있는 건의사항이나 다음 milestone을 위해 필요한 일 확인
3. **Ctrl+S**: 작업용 복사본(branch) 생성. 작업 하나 완료할 때마다 *commit*하기
4. **테스트**: 완료되면 *push*.
5. **반영 요청** (*pull request*)
   - Collaborators가 작업 내용 검토
   - 이상 없으면 *mainline*에 병합(pulled into the *mainline*)
   - 작업 로그 및 comment들도 같이 저장됨
6. **셔터 내리기**: 완료한 issue close하기.
7. **배포**: 모든 버그, 건의 등 반영됐으면 배포하기



- *pull*: 다른 branch (=version)의 코드를 가져오는 것
- *commit*: 현재 작업중인 branch의 변경사항을 local repository에 저장 
- *push*: 현재 branch를 remote repository에 저장
- *mainline*: main branch (= *trunk* or *master*). Stable branch와 development branch로 나누기도 함.

## 4.3. Best practices for scientific computing

>재현가능해야 한다 --> 올바른 습관을 기르기!



My top recommendations

- 계획 세우기: psuedo-coding
- 유지보수 용이하게: Modular
  - 하나의 기능 - 하나의 함수
- Version control system 사용하기
- 하나 만들때마다 테스트로 검증
- 주석은 해당 위치에

- 변수 이름 공들여서
- 코딩에 너무 공들이지 말기: 일단 무사히 실행하는 게 목적!



# 5. Introduction to Bayes

## 5.1. Confronting models with data

> 재현가능해야 한다 --> 데이터, 방법, 소프트웨어 투명하게 공개
>
> 오픈소스 소프트웨어 적극 활용합시다.



## 5.1. Confronting models with data



## 5.2. Probability 101



## 5.3. The likelihood



## 5.4. Bayes' theorem



## 5.5. Prior information



## 5.6. Numerical methods for Bayes



## 5.7. Evaluating MCMC output

