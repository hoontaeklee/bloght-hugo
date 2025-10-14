---
title: "Paper Review: Green (2017). Regional land-atmosphere Feedbacks. ng"
author: "Hoontaek Lee"
date: 2020-10-12T21:26:21+02:00
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

## 12 October, 2020 (Green, ng, regional feedbacks)

Green, J., Konings, A., Alemohammad, S. *et al.* Regionally strong feedbacks between the atmosphere and terrestrial biosphere. *Nature Geosci* **10,** 410–414 (2017). https://doi.org/10.1038/ngeo2957



## Overview

Here **the authors confirm land-atmosphere feedbacks** using satellite observations and a statistical method. The feedback from the biosphere to the atmosphere **explains 30% of variations in precipitation and photosynthetically active radiation (PAR)**. They employed **a multivariate conditional Granger Causality (MVGC) using vector autoregression models (VAR)** to decompose two directions in the feedbacks (i.e. atmosphere to biosphere and vice versa). Lastly, they explore how these feedbacks are represented in Earth system models (ESMs) and find that **ESMs underestimate the feedbacks**. 

**This paper is interesting** as it:

1. decomposed the feedback loop into each direction using an unfamiliar method
2. compared the feedbacks with those of ESMs to figure out flaws of the current ESMs, such as representing the photosynthesis and the biosphere's feedback in response to atmospheric forcing. 
3. 


## Feedbacks by each direction

![](/posts/figures/paper_review/2017_Green_fig1.jpg)

(**a, b**)

- Precip <-> **SIF** feedbacks appear in transitional regions between wet and dry conditions.
- positive effect of precip on SIF was resulted from dominating negative feedbacks (e.g. albedo) by positive ones.
- **a** and **b** show a similar distribution, meaning there are positive feedbacks (i.e. precip increase -> growth increase -> latent heat increase -> precip increase)

(**c, d**)

- PAR <-> SIF feedbacks appear in energy limited regions with extreme regimes (wet or dry), where the stomatal closure is not controlled by dry soil condition.
- This feedback is also positive (PAR increase -> growth increase -> sensible heat increase -> PAR increase)

**How can we decompose the contribution of positive and negative feedbacks?**

In **a** and **b**, the authors explained that positive feedbacks dominated negative ones. and in **c** and **d** they described increased sensible heat would increase PAR. 

**However, those explanations are based on the result.** They didn't explain how much the positive and negative feedbacks were and how much the effect of increased sensible heat and latent heat were (latent heat was also increased with PAR, which would reduce PAR by more cloud formation).

If they had quantified the each feedback process, they could have given more sound explanation.

***SIF** is used as a proxy of terrestrial productivity.



## ESMs representation of feedbacks

![](/posts/figures/paper_review/2017_Green_fig3.jpg)



ESMs underestimated the observed feedbacks.

- They systematically underestimated SIF -> Precip, and severely underestimated Precip -> SIF
- The SIF -> PAR feedback estimation varied for each model (i.e. under- or over-estimation)
- ESM **errors in representing the atmospheric forcing on the biosphere are even more severe** than errors in the opposite direction.
  - This implies that **ESMs are currently poor at representing photosynthesis and water stress sensitivities** of the biosphere and would be improved after correcting them.
  - This improvement is crucial for management decisions for food security, water supplies, and disaster management.



## Etc...

- The method of MVGC VARs can be implemented using a MATLAB Toolbox, or even using [an R package](https://towardsdatascience.com/a-deep-dive-on-vector-autoregression-in-r-58767ebb3f06?gi=f77c1ed21d76).

