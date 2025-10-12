---
title: "Paper Review: Green (2019). SMC-NBP"
author: "Hoontaek Lee"
date: 2020-09-11T16:37:00+02:00
description:
draft: false
hideToc: false
enableToc: true
enableTocContent: false
tocPosition: outer
tocLevels: ["h2", "h3", "h4"]
tags:
- 2020
- Paper Review
- Research
---

## 11 September, 2020 (Green, nature, SMC->NBP)

Green, J.K., Seneviratne, S.I., Berg, A.M. *et al.* Large influence of soil moisture on long-term terrestrial carbon uptake. *Nature* **565,** 476–479 (2019). https://doi.org/10.1038/s41586-018-0848-x

## Overview

The authors concluded that soil moisture has substantial effect on long-term net biosphere productivity (NBP, a.k.a. NEE?) using a global satellite product of SIF and TWS (GRACE) and multi-model ensemble from the GLACE-CMIP5 project. They explained that the SMC effect was attributable to non-linear response of NBP to SMC. Also, **they emphasized the need for better improvement representations of CO<sub>2</sub> fertilization effect in models**, as it is a basis of their results.




## SMC reduction and water-limited ecosystem

The authors decomposed changes in the total NBP into changes due to:

- dNBP<sub>SMvar</sub>: soil moisture variations from the climatological annual cycle (i.e. seasonal mean)
- dNBP<sub>trend</sub>: longer-term soil moisture trends (i.e. 30-year running mean)
- dNBP<sub>others</sub>: CO<sub>2</sub> fertilization and temperature effects
- error: all other limiting factors



![](/posts/figures/paper_review/2019_Green_fig1.jpg)



Figure 1:

- dNBP<sub>SMvar</sub> + dNBP<sub>trend</sub> (purple) remained negative during the period: SMC reduces NBP.
- Nevertheless NBP<sub>land</sub> increased until it met a peak: **dNBP<sub>others</sub> has significant effect.**
  - this means that **model representations of CO<sub>2</sub> fertilization effect is crucially important** for the projection.
- The contribution of dNBP<sub>trend</sub> (dNBP<sub>SMvar</sub>) gradually increased (decreased).
  - **Once an ecosystem put in a water-limited condition, the intra-annual variability becomes less effective.** 
- ESMs agreed that **there is a peak point for the global NBP**.



![](/posts/figures/paper_review/2019_Green_fig2.jpg)



Figure 2:

- All ESMs and observations (**i**) showed that **actual GPP exponentially (?) decreases when SMC becomes less than a certain amount (i.e. turning to the water-limited condition)**.
  - SMC decreases --> E decreases --> less cooling effect (temperature increases)
  - SMC decreases --> E decreases --> VPD increases --> stomatal closure --> photosynthesis decreases --> NBP decreases
  - SMC decreases --> (Ra / GPP) ratio increases + decreased photosynthesis --> NBP decreases
  - SMC decreases + increased temperature --> more fire occurrences --> NBP decreases
- Therefore, it is also **important to have realistic representations of vegetation responses to SMC reduction**.

<br>

Etc

- increased temperature lengthens the growing season length in mid- and northern latitude +
  reduced cloud coverage increases available radiation in **energy-limited** regions
  = remains as a CO<sub>2</sub> sink



## Methodology

Three experimental runs: a reference (CTL), ExpA, and ExpB

1. CTL: CMIP5 historic run + RCP8.5 scenario (SMC and CO<sub>2</sub> fertilization are accounted)
2. ExpA: CTL + mean climatological SMC forcing (seasonal mean SMC) --> remove soil moisture variability
3. ExpB: CTL + 30-year running mean SMC --> SMC trend

dNBP<sub>SMvar</sub> = dNBP<sub>CTL - ExpB</sub>: <u>exclude the effect of long-term SMC trend (?)</u>

dNBP<sub>SMtrend</sub> = dNBP<sub>ExpB - ExpA</sub>: <u>exclude seasonal variability to remain the long-term variability only (?)</u>

