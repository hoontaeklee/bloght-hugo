---
title: "Paper Review: Liu (2019). SAM->NEE across biomes. ELE"
author: "Hoontaek Lee"
date: 2020-05-01T13:43:04+09:00
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

## 1 May, 2020 (Liu, ELE, SAM->NEE across biomes)

Liu, Y., Schwalm, C.R., Samuels‐Crow, K.E. and Ogle, K. (2019), Ecological memory of daily carbon exchange across the globe and its importance in drylands. Ecol Lett, 22: 1806-1816. doi:[10.1111/ele.13363](https://doi.org/10.1111/ele.13363)



## Why did I read this paper?

To apply the SAM framework for my paper, I needed a reference. **Professor Ogle recommended this paper** for me as I and Liu et al. have the same type of data.

**This paper would be much more important than I expected** because 1) it contains **sample R code** in which the SAM was implemented; I would directly refer to it given I will use the same kind of data (i.e. observation with a fixed timestep), and 2) **it also proposes several critical questions related to my future PhD study at MPI-bgc** (i.e. water-carbon interactions across scales).



## What did they do?

The authors quantified the antecedent effect of some key factors on NEE. They used observations from **42 FLUXNET sites**, where met **some criteria** (e.g. data availability). The factors included 1) environmental factors (shortwave radiation, temperature, VPD, current SWC, antecedent SWC, PPT), and 2) biological factors (**unexplained NEE residuals by the environment factors**).



## Key findings

- **Environmental memory is necessary to explain variation in daily NEE throughout the year**

  - various time scales (shortest by shortwave radiation and SWC to longest by precipitation)
  - different responses by biomes (dry shrub lands versus forests)
  - **insensitive to the level of leaf growing**

- Another evidence for the local compensatory effect of water availability on photosynthesis and respiration (Jung et al., 2017)

  : the insensitivity to the level of leaf growing might be due to this local compensatory effect.

- **Scaling relationship** between environmental memory and water stress

  ![](/en/posts/figures/paper_review/2019_Liu_fig1.jpg)

- **Drylands may be more vulnerable to the future droughts**
  
  - Drylands showed more conservative strategy against resource deficit (i.e. longer-term memory)



## Possible limitations

- **The biological memory effect should be directly quantified**: The authors successfully considered the biological effects even without parameterizing them in the formula. The results however showed that the major contributor of the effect were **forest practices by human and natural disturbances** (i.e. insects). I could not fully agree that they are the biological factors the authors originally intended to investigate and **I think a method that can directly take the biological factors into account is required** rather than dealing with the unexplained residual by environmental factors.



## Notes

- **How does ecological memory at the daily scale propagate across other (and particularly, longer) time-scales to influence ecosystem carbon metabolism?**
- **How to assess ecological memory of component fluxes (e.g. photosynthesis and respiration)?**
  - But, the overall carbon exchange could be understood without this assessment given those component fluxes are compensated out (the local compensatory effect).
- The ability to predict land-carbon responses to future environmental changes rests upon an adequate mechanistic understanding of **how multiple processes and their interactions give rise to memory effects.**
- **Environmental memory integrates multiple processes**, therefore it could provides new insight into ecological responses at various time scales.
- **How does the scale relationship (i.e. memory vs. aridity) form across sites within multiple biomes?**
  - Physical delays driven by the movement of water?



## Next

I may further explore papers in which refer to the project paper (Jung et al., 2017) to get some idea for my PhD study.

