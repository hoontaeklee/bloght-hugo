---
title: "Paper Review: Humphrey (2021). smcAtmFeedback_NeeIav. Nature."
author: "Hoontaek Lee"
date: 2021-04-07T17:21:12+01:00
description:
draft: false
hideToc: false
enableToc: true
enableTocContent: false
tocPosition: outer
tocLevels: ["h2", "h3", "h4"]
tags:
- 2021
- Research
- Paper review
---

## 07 April, 2021 (Humphrey, Nature, smcAtmFeedback_NeeIav)

Humphrey, V., Berg, A., Ciais, P. *et al.* Soil moisture–atmosphere feedback dominates land carbon uptake variability. *Nature* 592, 65–69 (2021). https://doi.org/10.1038/s41586-021-03325-5



## Message: Soil moisture–atmosphere feedback dominates land carbon uptake variability

The same as the title.



## Novelty: putting the feedback concept in the discussion

Many studies have reported various factors such as SMC, Tair, and VPD, as the driving the global NEE IAV. This study reconciles these conflicting results by introducing a new common label to the candidates. SMC labeled as the **direct** effect while Tair and VPD had **the indirect** effect, as they are the spread of the SMC effect via **land-atmosphere coupling** (i.e. SMC --> LE --> Tair, Rh, VPD). **This labeling related the factors, which shifted the problem from finding the dominant driver to locating relevant drivers properly, which functioned as the reconciliation.**   



| <img src="/posts/figures/paper_review/2021_humphrey_fig1.jpg" style="zoom:100%;" /> |
| ------------------------------------------------------------------------------------- |



| <img src="/posts/figures/paper_review/2021_humphrey_fig3.jpg" style="zoom:100%;" /> |
| ------------------------------------------------------------------------------------- |



## Some questions

- Generality

  - Does the SMC-atm feedback drive **the global TWS IAV (and TWS-NEE IAV)**, too? If not, how much contribution from the feedback and what another dominator(s)?
    - apply the same analysis process to TWS (or TWS-NEE correlation) IAV data?
  - Can the same conclusion be drawn **at the regional scale**?
    - For example, the direct effect may be stronger than the indirect effect in snow regions (according to the figure 2b, c)
  - How does this conclusion change **in the future**? Does it remain as the dominator, too, or another dominator? 
  - Can **ML (or Hybrid) models** reproduce the same result?

- **The closure of a negative land-atmosphere feedback??**
  - SMC dec --> LE dec --> Tair, Rh, VPD inc (--> Photosynthesis dec) --> NEE dec --> TWS inc --> SMC inc (?)
  - Does the TWS  increase as NEE decreases? (expected, yes, as they are negatively correlated).
  - **Does the increased TWS result in the increase in SMC?** (we don't know how the TWS will be partitioned)
  - **How can we detect** this closure? (maybe, using historical time series?)
  - **Does this feedback affect the NEE (or TWS) IAV?** If yes, how and how much?
  - Is this related to the **tipping point of the Earth system**? (i.e. one feedback = one tipping, too strong feedback = never tipping again)



## Some phrases

> ET is the most efficient surface cooling flux

> Improving ESMs ... is essential for building confidence in projections of the long-term response of the carbon cycle to a warming and changing climate. ... it remains unclear whether temperature or soil moisture is the dominant driver of the inter-annual variability (IAV) in land carbon uptake at the global scale

> ... variability in soil moisture drives 90 per cent of the inter-annual variability in global land carbon uptake, mainly through its impact on photosynthesis. We find that most of this ecosystem response occurs **indirectly as soil moisture–atmosphere feedback**.

> ... NBP variability tends to be larger where LAC is stronger. These known **hotspots of LAC** match well with earlier studies that suggested that **semi-arid regions dominate global NBP IAV**...

- Other components in the feedback circle: ENSO and SST
  - **ENSO & SST** --> Tair and PPT --> SMC --> LE --> Tair, Rh, VPD --> Photosynthesis --> NEE
>  The **El Niño Southern Oscillation and SST** in general may be the confounding driver of both tropicalmean temperature and the precipitation patterns that cause the soil moisture anomalies leading to NBP variability.



