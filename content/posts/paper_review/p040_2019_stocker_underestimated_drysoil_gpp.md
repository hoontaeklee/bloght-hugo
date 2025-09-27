---
title: "Paper Review: Stocker et al., (2019). Underestimated GPP by RS models under dry soils"
author: "Hoontaek Lee"
date: 2022-02-19T14:46:17+01:00
description:
draft: false
hideToc: false
enableToc: true
enableTocContent: false
tocPosition: outer
tocLevels: ["h2", "h3", "h4"]
tags:
- 2022
- Research
- Paper review
---

## 19 February, 2022 (Stocker, ngeo, underestimated_drysoil_gpp) 

Stocker, B.D., Zscheischler, J., Keenan, T.F. *et al.* Drought impacts on terrestrial primary production underestimated by satellite monitoring. *Nat. Geosci.* **12,** 264–270 (2019). https://doi.org/10.1038/s41561-019-0318-6Introduction

Stocker et al. investigated the effect of dry soil on GPP across scales after isolating from the effect of VPD. I read this paper, wondering the global error distribution is associated with my global TWS IAV error map.  

## Message: Soil moisture should be included as a GPP estimator as VPD alone cannot account for dry soil impact on GPP

- Dry soil effect reduces the global annual GPP by 15%
- The effect of dry soil decreases with increasing spatial scale, due to compensation from different regions.
  - validated by symmetric pattern of histogram of soil moisture effect across the globe.
  - **it was interesting that the compensatory perspective is applied here as well**

## Global distribution of soil moisture effect on the global GPP IAV

| <img src="/en/posts/figures/paper_review/2019_Stocker_figS9.png" style="zoom:100%;" /> |
| ------------------------------------------------------------ |

- Values were calculated following Ahlstrom et al. (2015)
- I can see that most of hotspots of the global TWS IAV errors have strong amplification of GPP IAV by dry soil (e.g., the Parana basin).
- But also some of hotspots didn't show a clear sign (e.g., lower Mekong basin).

| <img src="/en/posts/figures/paper_review/2019_Stocker_figS10.png" style="zoom:100%;" /> |
| ------------------------------------------------------------ |

- Again, semi-arid regions pop up. 

## *fLUE*, a metric to quantify the bias from soil moisture effect

[Stocker et al. (2018)](https://doi.org/10.1111/nph.15123) separated SM effect on GPP from VPM effect on GPP using neural network (NN), a magical blackbox.

They trained two kinds of NN to predict LUE. One learned from **T, VPD, and PAR**, the other one learned from **T, VPD, PAR, and SM**. So, the difference or ratio can be used as SM-alone effect on GPP.

*fLUE*  excellently quantifies and corrects model bias (e.g., Figure 1b).

## Behind the paper...

Stocker wrote [an interesting post](https://stineb.netlify.app/post/soilm_global/) about the background of this paper; most of them are well-described in the introduction of this paper as well.

- **Remote sensing cannot nicely monitor soil moisture.**
  - or only limited to the very shallow layer (~5 cm)
- So, **many RS-based approaches rely on LUE model to estimate GPP**
  - GPP = PAR * fAPAR * LUE
  - PAR reflects light-GPP relationship
  - fAPAR includes the effect of vegetation greeness, so does that of phenology and mortality which drought are one contributor to.
  - LUE covers differences in leaf-level physiological responses.
  - LUE is commonly modelled using vegetation properties, air temperature, and **VPD**
- **It has not been clear if VPD can represent the whole SM effect or not, and thereby further impact of the bias is not clear, either**

## etc

An on-going challenge to monitor soil moisture and its effect on Earth system:

> Directly using soil moisture as an input to RS models has thus far been hampered by data availability with global coverage. New soil moisture data products that are based on microwave remote sensing47 may resolve this constraint but are generally representative only for upper soil layers
> (which limits their applicability to deep-rooted vegetation) and are subject to data gaps in regions with dense vegetation cover47. **Recent**
> **efforts to estimate root-zone soil moisture48 combined with estimates of the global distribution of plant rooting depth49 may prove useful to address these limitations.**



A possible role of water storages other than ones in shallow soil layers:

>We further found **a compensatory role of water limitation in different regions** that leads to a reduced apparent soil moisture effecton IAV in global GPP. This reflects earlier work that found a declining importance of water availability on GPP and the land C balance when moving from local to global scales. However, we note that the model used for our analysis, as well as the one used by ref. 54, accounts for only relatively shallow soil water storage, **without accounting for the possible role of other types of water storage that may be relevant for vegetation productivity (groundwater, for example), control its interannual variability and may preserve a strong soil moisture effect on C cycle variability at the global scale.**
