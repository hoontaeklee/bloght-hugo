---
title: "Paper Review: Gentine (2019). Coupling between carbon and water cycles-a review. erl."
author: "Hoontaek Lee"
date: 2020-11-16T22:32:26+01:00
description:
cover: 
  relative: true
draft: false
hideToc: false
enableToc: true
enableTocContent: false
tocPosition: outer
tocLevels: ["h2", "h3", "h4"]
tags:
- Research
- Paper Review
- 2020
---

## 14 October, 2020 (Gentine, erl, cw coupling)

Gentine, P., Green, J.K., Guérin, M., Humphrey, V., Seneviratne, S.I., Zhang, Y., *et al.* (2019). Coupling between the terrestrial carbon and water cycles—a review. *Environ. Res. Lett.*, 19. https://doi.org/10.1088/1748-9326/ab22d6



## Overview

The right topic for my project.

The authors wrote that this paper would be an introduction of the coupling of carbon and water cycles to people who are not familiar with. Indeed I think they summarized the topics nicely with well-organized structure. 

Here I would like to write down some points from each section in the paper.



## Atmospheric versus surface coupling

**GHG** effect and physiological responses of vegetation (e.g. **stomata**) convey atmospheric influences to changes in **energy, water, and carbon cycles** on the biosphere.



## Surface CO<sub>2</sub> effects on vegetation

The effect of [eCO<sub>2</sub>] over ecosystems were intensively investigated by the **FACE** (Free-air CO<sub>2</sub> enrichment) experiments.

Increased atmospheric CO<sub>2</sub> concentration [eCO<sub>2</sub>] typically:

- decreses stomatal conductance.
- increases CO<sub>2</sub> gradient between intercellular and leaf surface.
- increases biomass production (i.e. **greening**).
- alters belowground biomass (e.g. fine root). <-- **technically more challenging**
- resulted in taller with larger diameter, more branches and leaves.



C3 species are expected to more sensitive to [eCO<sub>2</sub>] then C4 species (photosynthesis and transpiration).

- C3 species uses RuBisCo as an enzyme for assimilation.
- C4 species adds another enzyme, PEP carboxylase. **They release CO<sub>2</sub> into the bundle sheat cells, where CO<sub>2</sub> concentration is pretty high even without [eCO<sub>2</sub>] condition**.



**Land management** could be the major cause of the CO<sub>2</sub> fertilization effect has confirmed so far. 

- most of the observed greening across the globe appears to be located in regions of strong land management.



## Soil moisture effects on water-carbon coupling

- **SMC↓** --> **gs↓, cAlloc↑↓, embolism↑**
  - embolism: sap flow blockage due to air bublle formation in the xylem)
- **SMC↓** --> cell growth↓ (xylem and phloem) --> **Tr↓, GPP↓**
  - xylem sap water is used to replace transpired water in leaves
  - xylem and phloem interact through changes in osmotic pressure and water potential, regulating the water and carbohydrate transports in the plant.
- **SMC↓** --> cavitation↑ (--> defense↓) --> mortality↑ --> **Tr↓, GPP↓, Rh↑**
- **SMC↓** --> gs↓ --> ET↓ (--> H/ET↓) --> VPD↑, **Tsurf↑** --> gs↓
- **SMC↓** --> **sap conductivity↓** (of new xylem; transport efficiency)
  - at the expense of safety
- **SMC↓** --> solute transport↓ --> microbial activity↓ --> **Rh↓**
  - vs. **SMC↓** --> Esoil↓ --> Tsurf↑ --> **Rh↑**
  - SMC↑↑ --> O<sub>2</sub>↓ --> **Rh↑**



## VPD effects on vegetation

leaf-level (well understood) 

- VPD↑ --> gs↓
  - to **maximize GPP/Tr**, while **maintaining underlying WUE** (WUE VPD<sup>1/2</sup>)

**ecosystem-level (poorly understood)**

- Due to **the strong coupling between VPD and SMC**
  - the coupling limits carbon uptake and triggers mortality.
- VPD↑ --> fire↑ --> GPP↓



## Water use efficiency = GPP/Tr

Factors affecting WUE:

- [eCO<sub>2</sub>]
- VPD
- gm
- the degree of land-atmosphere coupling
  - ecosystem conductance
  - aerodynamic roughness

**The influence of soil moisture on long-term (year to decades) WUE has rarely been assessed, likely because of the challenges in continuously measuring and disentangling the effects of confounding factors such as VPD.**



## Extremes

Extremes (e.g. droughts and heat waves) substantially affect the terrestial water and carbon cycles:

- **Carbon cycle IAV, especially in transitional climates (monsoonal or semi-arid)**.
  - SMC and temperature are the key regulator on carbon uptake over the regions.
- **Legacy effect** (e.g. a large-scale die-off)



## Global soil moisture impact on carbon cycle

**At the individual level**, soil moisture affects 

- gs sensitivity to VPD
- enzyme activity (photosynthesis and respiration)

**At the global scale**: 

- **The soil moisture effect on carbon cycle, especially on ecosystem and global scales, is still less understood mostly due to lack of direct observations.**

soil moisture effects **in models** --> **empirical regulations of stomata conductance (gs)**

- beta factor (wilting point and field capacity)
- atmospheric dryness dependence (i.e. VPD effects on gs)
  - based on a **stomatal optimality principle (i.e. maximize GPP/Tr)**
- challenge: **soil moisture vs. VPD**: they show a strong negative relationship
  -  **Chunhui's project**
  - Liu et al., 2020: Soil moisture !!! vs. Novick et al., 2016: VPD!! ... (**under debate**)
- mostly omit the xylem and phloem connection
  - exceptions: Xu et al., 2016, ...

Data

- in situ: **extreme SMC values are important on GPP and NEE.**
- Satellite: new opportunities for understanding at global scale 
  - SIF: proxy for GPP, NEE, Phenology, Tr, ...)
  - SMC: monitoring drought effect, ecosystem resilience, ...
  - TWS: GRACE

> Global GRACE TWS changes were recently found to be strongly correlated to anomalies in global land carbon uptake, highlighting the potential of GRACE TWS observations for understanding water-carbon cycles' coupling.

... How to nicely utilize the relationship? 

The soil moisture variability impacts on the simulation of global NBP

- **Non-linear response of NBP to soil dryness causes the damage by drought cannot be compensated by positive soil moisture anomalies (Green et al., 2019).**



> observations based on SIF and GRACE TWS emphasize the strong coupling between carbon and water, but mostly in the transitional dry-wet (semi-arid and monsoonal) regions as have already highlighted in previous studies (Poulter et al., 2014, Ahlstroem et al., 2015, Zhang et al., 2016).



**ESM-simulated GPP is more sensitive to soil dryness stress compared to observations**.

- Land-surface models are known to exhibit a dry bias, <u>because soil moisture decays too fast</u> and this decay stresses ecosystems too much, <u>with little resilience</u> based on deep rooted water.
- **Long-term feedbacks between the carbon and water cycles** (i.e. <u>memory and legacy effects</u>) are mainly absent from ESMs
  - Soil moisture regulates plant growth, and especially <u>sap area and tree ring size</u> on interannual time scales, with wet years leading to larger tree rings, <u>which impacts the amount of transpiration and photosynthesis</u>.
  - Moisture availability affects the <u>allocation</u> to different carbon pools.

At the global scale there has been **a debate on whether temperature or water availability plays the preponderant role on biosphere carbon cycling**.

- Temperature effects dominate global NBP (Jung et al., 2017).
- Water storage impacts global NBP (Humphrey et al., 2018).
  - **A lack of long-term memory in soil moisture** would explain why global effects of water stress on carbon cycle IAV seem to be underestimated.



## Global CO<sub>2</sub> impact on water cycle

**ESMs could naturally account for land-atmosphere feedbacks**, which lacks in FACE observations.

- Disentangle with different [CO<sub>2</sub>] input (surface vs atmospheric vs both)



GHG effect vs physiological effect (surface [CO<sub>2</sub>])



The GHG effect (i.e. radiation↑, temperature↑) on **ET**

- decrease in dry regions
- increase in wet or cold (snowy) regions where higher temperature increases snowmelt and can extend the growing season length



[eCO<sub>2</sub>] effects on **ET** in ESMs:

- Typically negative due to the higher WUE)
- tropical: [CO<sub>2</sub>]↑ --> LAI↑ >> gs↓ --> ET↑
- others: [CO<sub>2</sub>]↑ --> gs↓ >> LAI↑ --> ET↓



[eCO<sub>2</sub>] effects on **SMC** in ESMs:

- dry regions: [CO<sub>2</sub>]↑ --> SMC↓, ET↓ - gs↓ (compensation by stomatal closer)
- wet forested regions: [CO<sub>2</sub>]↑ --> SMC↓ (due to increased atmospheric demand)



[eCO<sub>2</sub>] effects on **the water cycle** in ESMs: (**should be improved**)

- WUE
- gs
- biomass & phenology



## Discussion and challenges

The terrestrial water-carbon cycles have to be studied as **an interconnected system**.

Surface [CO<sub>2</sub>] is a dominant control of the future water cycle and **the representation of vegetation water stress places key constraints on the capacity of continents to act as a future CO<sub>2</sub> sink**.

Numerous challenges:

- limited observations to constraint **[eCO<sub>2</sub>] effect on ecosystem WUE change**
  - isotopic inferences
  - eddy covariance
  - remote sensing
- [eCO<sub>2</sub>] effect on **LUE change**
- **partitioning ET** into E and T
- **Water stress effect constraint at the global scale** 
  - RS
  - SIF
- **Ecosystem respiration at the global scale**
- **VPD-SM coupling** and effects on photosynthesis by each
  - new statistical tools? (Granger causal analysis, )
- **Coupling of water and carbon cycles at inter-annual and decadal scales**
  - short (leaf-gas exchange) - annual (carbon allocation, xylem changes) - interannual (species composition, mortality, legacy)
  - long-term RS & in-situ observations
- Predictions under more frequent **extreme  events**
- **land management**
  - effects on the Earth greening
  - the pressure on food production due to rising population and increased temperature and VPD pressure on crop production
  - ESMs will be more important tool
