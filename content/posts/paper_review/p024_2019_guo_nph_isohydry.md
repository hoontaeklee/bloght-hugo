---
title: "Paper Review: Guo (2019). SAM->iso/anisohydry. NPH"
author: "Hoontaek Lee"
date: 2020-05-20T21:16:35+09:00
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

## 20 May, 2020 (Guo, NPH, SAM->iso/ansiohydry)

Guo, J.S., Hultine, K.R., Koch, G.W., Kropp, H. and Ogle, K. (2020), Temporal shifts in iso/anisohydry revealed from daily observations of plant water potential in a dominant desert shrub. New Phytol, 225: 713-726. doi:[10.1111/nph.16196](https://doi.org/10.1111/nph.16196)

## A key reference for applying the SAM framework

I have reviewed a [paper](/posts/paper_review/p023_2019_liu_ele_SAM_NEE) in which the SAM framework was applied to fluxtower NEE data. I read the paper because I used a similar type of data (i.e. fluxtower GPP and ET). **However**, after looking into the source code by Liu et al. (2019), I have found that it was more complicated than one I want to implement.

**Instead**, I found this paper. Guo et al. provides an excellent reference case **with relevant R & JAGS source** **code** of sufficiently complex design.

**Conclusions about the advantages of iso/anisohydry** from this paper are **not that unique**: isohydry helps trees to exploit the favorite environmental condition, whereas anisohydry makes them to survive during the dry condition. **However**, the authors could derive which environmental drivers affect those responses thanks to the SAM framework.

## SAM framework quantifies the effects of environmental drivers to parameters in a model.

It was interesting that the SAM framework can be used to quantify the weight of effectiveness of drivers to model parameters as well as to a dependent variable. The authors could estimate **time-varying parameter values and the relevant weights**. Also, the framwork could be applied to quantify effects of drivers **across various spatio-temporal scales**, which could probably a key technique of my research.

**Via inspecting the resulted weights of environmental drivers**, they confirmed that the shife between iso/anisohydry was influenced immediately by soil water and slowly by temperature. **Also**, they found that the shift from isohydry to anisohydry in winter was caused by low temperature, not by low moisture content, **referring highly negative weight of temperature during that time**.

## The Martinez-Vilalta framework

The MV framework is simple, but surprisingly outperformed to simulate midday water potential.

It is a simple linear regression:

MD = sig x PD + gam

where MD is midday water potential, PD is predawn water potential, and sig and gam are the slope and intercept, respectively.

**The sig varies from 0 (isohydry) to higher values (anisohydry).**

The MV framework with time-varying parameters could provide better estimates of the MD then the model with time-static ones.

## Plasticity is related to the superior fitness

This study described that the *Larrea* could successfully survive from dried region as it can **flexibly shift between iso/anisohydry along with the environmental condition**. They could be an anisohydry when the conditions are good, while they turned to isohydry with a harsh condition.

This may be a similar message with that a tree species can succeed in **surviving during drought with flexibly adjust the water uptaking depth**.