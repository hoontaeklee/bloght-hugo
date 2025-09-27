---
title: "Research Topics"
author: "Hoontaek Lee"
date: 2020-02-10 11:34:48+09:00
publishdate: 2020-02-10 11:34:48+09:00
lastmod: 2020-06-26 10:02:48+09:00
draft: true
tags:
- 2020
---

# Optimal temperature for photosynthesis

- LI-6400으로 광합성 측정할 때 잎 온도를 25도로 설정한다. **광합성 최적 온도**(optimal temperature for photosynthesis, OTP)가 일반적으로 25도라고 알려져있기 때문.
- Kumarathunge et al. (2020, https://doi.org/10.1111/gcb.14975)은 **OTP가 수분 상태에 따라 달라진다**고 보고했다.
  
  - 수분 조건이 충분할 때 3도 높았다.
- **OTP에 영향을 미치는 다른 조건**도 있을 수 있다.
  - nutrient (N, P, ...)
  - species
  - age
  - disturbances (drought, heat extreme, fire, herbivore, disease, ...)
- OTP가 미치는 영향
  
  - 시공간 규모를 달리 했을 때? (**model simulation** results)
  
    

# Non-structural carbohydrates (NSC)

**1. How much NSC is needed to recover from hydraulic failure (or carbon starvation)?**

- Does the cost of recovery differ between each damage?

**2. How large is the NSC pool size? (or concentration)**

- Actually, NSC exists all around the tree like the blood in human body. But depicting this form in models is difficult, so modelers depend on the pool concept.

**3. How can we measure the NSC in non-destructive and automatic way?**

- It is currently measured by a destructive and manual way.

**4. How can we add the NSC to satellite product?**

- To benefit from the extensive spatial coverage of the satellite.



나무에게 NSC는 농업에서 저수지, 인간 사회에서 가용 현금(**비상금**)으로 비유할 수 있다.

나무는 비상 사태(가뭄, 폭염, 서리, 충해 등)가 발생해 탄소 수급에 차질이 생기면 기존에 저장해 뒀던 NSC를 끌어와서 부족한 탄소량을 충당한다.

비상 사태의 종류나 피해 정도에 따라 나무가 얼마나 피해를 입고 견딜 수 있을지 정량화 할 수 있을까.

그러려면 나무가 가지고 있는 NSC의 양과 각 피해마다 복구에 필요한 NSC의 양이 얼마나 되는지 정량화 할 수 있어야 할 것이다.

이를 정량화 하고 나면 현재 그 나무가 얼마나 피해를 견딜 수 있을지를 파악할 수 있을 것이다.

그리고 숲에서도 인간 사회에서처럼 빈익빈 부익부 현상이 나타나는지 확인하는 등의 연구도 가능할 것이다.

예를 들면, 각 재해 종류마다 복구하는 데 1 unit의 NSC가 필요하다고 가정해보자. 한 나무의 NSC가 2라면 두 번의 피해를 복구할 수 있는 것이다.

견딜 수 있는 피해의 횟수(N)가 큰 나무일 수록(우점할수록) N이 매우 커지는 반면, 피압된 나무는 N이 1 미만인 것으로 빈익빈 부익부 현상을 확인하는 것이다.

그리고 그 이후에는 N의 개체별 분포를 고르게 만들어서 빈익빈 부익부 현상을 완화하고 전체적으로 더 튼튼한 숲을 만들게 되는 것이다.

(하지만 이는 결국 개체별 광합성량을 조절해야 하는 문제이기 때문에 실현하기는 힘들지도 모른다)



# Mountainous terrain effects on cycles

> mountainous terrain, complex terrain, or topographic effect



**Context**

- The topographic effects on water and carbon cycles across various scales are uncertain.
- Currently, TBMs depict the numerical world as flat one. (**<-- really?**)
- A large part of the forest ecosystem locates in mountainous regions.
- The mountainous region has some different conditions with those of plain.
- This discrepancy may cause uncertainties in simulations of TBMs

**What is the mountainous terrain?**

\- **dry soil**: shallow soil layer, rapid percolation

\- **carbon allocation**: shallow rooting depth vs stronger wind speed, less competitive for light

\- **nutrient condition**: mother rock (source of nutrient such as phosphorous)

\- **weather conditions**: more rainfall, stronger wind (-> boundary layer conductance), low temperature (high elevation),

**Questions**

- How important is the terrain effect?
- How many TBMs consider complex elevation distribution such as in mountainous region?
- How can MT be integrated into TBM?
- How different are the characteristics of trees between MT and plain?
- Which are the characteristics that show substantial uncertainty and need to be improved?

After integrating MT into TBMs ...

- How different in surface energy fluxes?

- How different in the carbon budget for each biome and for the globe?

- How differently respond to climate change?

  

# Examining the JULES phenology model over biomes

- **Does the JULES phenology model appropriately estimate the leaf area index of different biomes in the globe?**

- **What are the causes of errors in LAI estimates of the JULES phenology model and how can the model be improved?**

- **How does the improved JULES phenology model affect simulations of land-atmosphere exchanges (e.g. energy flux and carbon cycle)?**



# Examining impact of different processes at a small scale on cycles at various larger scales and their interactions

- **Does the propagation look different between different models?**
- **Does the propagation look different between models and observations?**
- Which process? + which approach/expression for depicting the process? (target of comparison)
  - leaf scale? tree scale? ecosystem scale? global scale?
  - leaf scale
    - can provide information that which process affects which process
    - which process needs to be improved (priority)
- Which cycles to test the impact?: water and carbon only? any other potential cycles? (e.g. nitrogen)



# Applying the SAM framework

- **Are antecedent effects of environmental and biological variables different by** 
  - **the source of LAI, GPP, and ET (e.g. satellites, phenology models, and  measurements)?**
  - **scales?**
- 



# Maximum entrophy approach for simulating ecosystems



- **How can the maximum entrophy concept be used for simulating ecosystems (e.g. forest ecosystem and Earth system)?**
- I think that the entrophy concept could probably be applied to simulate the (terrestrial) ecosystem.
- Now, I have seen that the maximum entrophy approach is used in the species distribution modeling (i.e. the Max-Ent model).



# Potential increase in uncertainty with increaesing Tropical forests under climate change



- **What will be the fate of the uncertainty in functioning of the Earth system?**
- Tropical forests are the major source of uncertainties in simulating the Earth system (Cano et al., 2020; ...), and their area is anticipated to be increased (...). 
- At the same time, changes in areas of other biomes are also expected.
- Because the contribution of each biome to the simulation uncertainty is various, changes in portions of biomes may be affect the performance of simulation.



# Disclosing the other side of a coin: what has the South Korea been lost after they succeeded in a government-driven greening campaign.   

- **단일 수종 녹화사업을 진행한 후 무엇을 잃었을까?**

- 최근 미국의 한 연구진은 칠레 사례를 들어 **대규모 조림사업이 오히려 부정적인 결과를 가져올 수 있다**고 발표했다(https://www.sciencedaily.com/releases/2020/06/200622133012.htm; https://www.nature.com/articles/s41893-020-0547-0).

- 조림 정책의 디자인이 올바르지 못하면 **생물다양성 감소, 토착종/외래종 비율 감소, 탄소 저장량 감소** 등의 결과를 초래할 수 있다.

- 우리나라는 산림 녹화에 성공한 대표적인 국가이다. 해당 녹화사업에서는 척박한 토양에서 견딜 수 있는 수종을 선택해야 했기에 몇 가지 수종으로만 **조림 수종이 한정되었다.**

  - 어쩔 수 없는 선택이었기 때문에 그 때 그 선택이 잘못됐기보다는 앞으로 가능한 선택끼리 비교하는 게 맞다?(조림 시나리오별 생물다양성, 탄소저장량, 재해(가뭄, 폭염, 병충해, 산불, ...)에 대한resilience&resistance ... 등 시뮬레이션)

- **가까운 미래에 시행 될 조림사업에서 가능한 선택지에 따른 결과를 비교하고 어떤 선택을 해야 할지 방향을 제시할 수 있다.**

  

# Various temporal scales over which antecedent variables affect different biomes and the resulted differences in fluxes.

- Why do different biomes have different temporal scales over which they respond to antecedent variables?
  - Samuels-Crow et al (2020, JGR-bg): in its discussion, they said that the arid region showed the longest memory.
- What will be the effect of the difference on water and carbon cycles across scales?
  - At least we can explore the results of the scale difference via simulations even though we do not know the reason behind the difference.
- 

