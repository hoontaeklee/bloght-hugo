---
title: "Paper Review: Jung (2020). FLUXCOM evaluation: carbon. bg."
author: "Hoontaek Lee"
date: 2020-12-26T22:45:07+01:00
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

## 27 December, 2020 (Jung, bg, FLUXCOM carbon)

Jung, M., Schwalm, C., Migliavacca, M., Walther, S., Camps-Valls, G., Koirala, S., Anthoni, P., Besnard, S., Bodesheim, P., Carvalhais, N., Chevallier, F., Gans, F., Goll, D. S., Haverd, V., Köhler, P., Ichii, K., Jain, A. K., Liu, J., Lombardozzi, D., Nabel, J. E. M. S., Nelson, J. A., O'Sullivan, M., Pallandt, M., Papale, D., Peters, W., Pongratz, J., Rödenbeck, C., Sitch, S., Tramontana, G., Walker, A., Weber, U., and Reichstein, M.: Scaling carbon fluxes from eddy covariance sites to globe: synthesis and evaluation of the FLUXCOM approach, Biogeosciences, 17, 1343–1365, https://doi.org/10.5194/bg-17-1343-2020, 2020.

## Overview

This is **a review paper of the FLUXCOM products of the carbon cycle** (i.e. GPP and NEE). As **I will use the FLUXCOM products** for my project, it would be better to know about how it was structured, how well it performs, and what current issues are. **Martin described thoroughly** about the results and the relations (results from other researches, possible limitations, ...). **I could feel how deeply he contemplated** about the results. I could point out **some subjective bullets** here:

1. Generally, the FLUXCOM performs well about estimating the mean annual value or seasonal pattern of GPP and NEE while **it  poorly works in estimating the interannual variation** of them.
   - Maybe, this is why they employed me for the project.
2. **There was no section for R<sub>eco</sub>**. This means there are not enough observations to train ML models for R<sub>eco</sub>. 
3. I will expect the **water cycle version** of this paper.



## Schematic overview of the FLUXCOM initiative

![](/posts/figures/paper_review/2020_jung_fig1.jpg)



The FLUXCOM product consists of RS and RS+METEO products:

- RS: fluxes are estimated **exclusively** from MODIS. 0.0833 deg, 8 d, 2001-2015
- RS+METEO: fluxes are estimated from **mean seasonal cycles** of satellite data and daily meteorologicla information. 0.5 deg, daily, temporal coverage is up to the meteo. input.
  - using mean seasonal cycles only is **linked to the underestimation of IAV** by RS+METEO

Refer to Tramontana et al., 2016 and Jung et al., 2019 for more information.



## Atmospheric inversion-based estimates

This is an independent product of **top-down** method. I have heard many times this in group meeting but couldn't understand. I may need to refer to the literature further, e.g. Roedenbeck et al., 2018.



## GPP

- After mentioning a topic, Martin describes how other studies concluded for the same topic with which reasons. This each description seems to be able to be regarded as a piece of **literature review**. 

> We need to acknowledge that global GPP is largely driven by the productivity in the **tropics**.

> In conclusion, global FLUXCOM GPP estimates are within the currently most plausible **110-150 PgCyr<sup>-1</sup>** range.

> a range of NPP:GPP ratios of **0.4-0.55**



## NEE

### Mean annual NEE

> a particularly large systematic difference in the tropics (...) this is a systematic feature of the current data-driven approach.

> a sizable carbon sink in intact tropical forests ... offset by carbon loss pathways such as fire, LUC, (...) These CO2 sources are not sampled by EC measurements (...) **these secondary carbon loss fluxes do not dirve the large discrepancy** between FLUXCOM and inversion-based mean net carbon exchange.

> clearly, more tropical EC sites are needed.



### Seasonal cycles

> a good consistency between FLUXCOM and inversions

> adjusting inversion-based NBP towards NEE by **correcting for fire emissions does not improve the correspondence with FLUXCOM in tropical** and subtropical regions.



### IAV

![](/posts/figures/paper_review/2020_jung_fig8.jpg)



> the **hotspots** in Southeast Asia, southern North America and also the Siberian tundra.

> Overall, there are still differences in the spatial patterns of IAV magnitude among and within different data streams.

> the choice of machine learning method, rather than meteorological forcing data, has a larger influence on IAV of global NEE.

> ML methods can benefit from higher temporal variability.

> Overall there are **large discrepancies** between FLUXCOM and TRENDY as well as amongst TRENDY models with respect to **local NEE IAV**. This reflects **our limited understanding and capabilities to model year-to-year variations in local ecosystem carbon exchange**.

>However, both approaches yield **good correspondence of globally integrated NEE**

- the spatial compensation of locally important processes



## Limitations and potential ways forward

### site history

>The current limitations of unrealistic mean NEE patterns from FLUXNET upscaling are also due to missing predictor variables that describe **site history effects**

- Here, there are some paragraphs about literature review of some studies.
- How to properly consider the site history?



### CO<sub>2</sub> fertilization

>FLUXCOM lacks any explicit treatment of the effects of CO2 fertilization, causing carbon flux trends to be unrealistic



### water stress

>we should strive further to improve water stress effects in the upscaling approach given its significance

>Unfortunately, current soil moisture products from remote sensing are only representative of the top few centimetres and are at comparatively **coarse spatial resolution**

>Perhaps the larger issue is diverse **ecosystem-specific responses** to soil moisture variations



### Machine learning

> **RNNs were designed for time series** and can account for dynamics such as ecosystem **lag and memory effects** on carbon flux variability.

> Conceptually, lag and memory effects emerge due to the effect of unobserved ecosystem state variables.

> **CNNs**, in particular, have proven to be very powerful, especially for **image processing and recognition tasks**

> **combining CNNs with transfer learning approaches seems very promising** from a conceptual perspective. The principle of transfer learning is to learn relevant features from a more densely observed proxy variable of the actual target and use the feature representation for learning the target. (...) This approach could be applicable to the upscaling of FLUXNET GPP by using remotely sensed SIF as a proxy and thereby alleviate issues related to small sample size (e.g. extrapolation) but also aid
> the **extraction of small but relevant signals (e.g. IAV)**.

- CNN + transfer learning