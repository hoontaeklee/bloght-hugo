---
title: "Paper Review: Green et al., (2022). LST/Tair, a remote sensing-based indicator of vegetation water stress"
author: "Hoontaek Lee"
date: 2022-04-20T21:56:26+02:00
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

## 23 April, 2022 (Green, gcb, lst_over_tair) 

Green, J. K., Ballantyne, A., Abramoff, R., Gentine, P., Makowski, D., & Ciais, P. (2022). Surface temperatures reveal the patterns of vegetation water stress and their environmental drivers across the tropical Americas. *Global Change Biology*, *28*(9), 2940–2955. https://doi.org/10.1111/gcb.16139

Green et al. introduced the ratio of land surface temperature (LST; temperature of the top canopy) to air temperature as an indicator of vegetation water stress. I was particularly interested in their analysis using **random forest and the Shapley value** to quantify the effect (e.g., pushing to above the mean) of each timestep on the target variable (i.e., LST/Tair). This paper was interesting to read, as the indicator is not only based on (satellite) observations but also based on a solid theory.

## Message: LST/Tair with machine-learning approach can detect vegetation water stress

## Random forest with Shapley value

Random forest is so far the favorite machine-learning algorithm for me because it is not just a black-box model; it provides us the feature importance. With deploying the Shapley value, this bacomes more powerful. It can quantify the importance of **each timestep**, as well as the variable (as the sum of importance of timesteps).

I thought that this way is what I need for my first study. I could spatially attribute the global variance of a variable, so that I can identify the hotspots (i.e., a group of major contributors), but I relied on empirical or simple analyses for the temporal attribution. **With this RF+Shapley method, I can spatially and temporally attribute the global variance, so that I can detect not only hotspot pixels, but also hot timings as well with the effect quantified.** 


## etc

I didn't like the boxes they used to describe their work flow and relevant hypothesis. The box showed us the workflow, but didn't include the hypothesis. The authors usually mention the box together with the corresponding hypothesis. It was not easy for me to remember the corresponding hypothesis so I had to go back to the end of introduction.
