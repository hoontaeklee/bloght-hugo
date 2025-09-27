---
title: "Paper Review: Holgate (2016). SMC. RSE"
author: "Hoontaek Lee"
date: 2020-02-27T20:00:00+09:00
publishdate: 2020-03-01T16:46:00+09:00
description:
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

## 27 February, 2020 (Holgate, RSE, SMC)

Holgate, C.M., De Jeu, R.A., van Dijk, A.I.J.M., Liu, Y.Y., Renzullo, L.J., Dharssi, I., Parinussa, R.M., Van Der Schalie, R., Gevaert, A., Walker, J., 2016. Comparison of remotely sensed and modelled soil moisture data sets across Australia. Remote Sensing of Environment 186, 479–500.



### Summary

This paper compared time series pattern and temporal anomaly of diverse soil moisture content (SMC) products with in-situ measurements. The methodologies included the Pearson correlation coefficient, an anomaly index and the cluster analysis. By comparing in a common frame, this study could provide a glimpse of the performances of the SMC products. **I would probably refer to this paper**, as I would like to compare many ET and SMC products.



### Controversy about KBDI

![](/en/posts/figures/paper_review/2016_Holgate_table3.jpg)



![](/en/posts/figures/paper_review/2016_Holgate_fig8.jpg)

--> The authors pointed out that the KBDI dried down too slowly after days of wet condition, which might be the cause of low correlation value. **However**, in my case, KBDI shows a good agreement with in-situ SMC observations without any slow responses after wet conditions.



### Other comments

- I think it is **a nice way of starting the section** 4.3.: "**The purpose of this section is to** summurise the main features of interest within the time series"
- I am interested in **the two modelled indices**: API (antecedent precipitation index) and MSDI (Mount's Soil Dryness Index). **API** showed a great performance although it has a very simplified structure and calculation (temperature and precipitation). **MSDI** seems as an upgraded version of KBDI as it additionally accounts for vegetative factors of each PFT.
- Model-based products showed better performances than satellite-based ones. **How could this be possible?** The authors in the discussion only stated about spatial scale and the number of points.
- In the first section of the discussion, results of other studies about inter-comparing a variety SMC products were summarized. **How those papers including this one could be published even all these were about comparing SMC products?** Were there different implications among the studies?