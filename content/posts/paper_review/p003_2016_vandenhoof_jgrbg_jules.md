---
title: "Paper Review: Van den Hoof (2016). JULES. JGRBG"
author: "Hoontaek Lee"
date: 2019-04-27T20:00:00+09:00
publishdate: 2020-03-01T16:28:00+09:00
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
- 2019
---

## 27 April, 2019 (Van den Hoof, JGRBG, JULES)

Van den Hoof, C. and Lambert, F. (2016). Mitigation of drought negative effect of ecosystem productivity by vegetation mixing. **_Journal of Geophysical Research: Biogeosciences_**, 121, 2667–2683.  

This paper conducted an interesting numerical experiment to investigate changes in SMC and Carbon & Water fluxes by vegetation mixing. This vegetation mixing was represented by adjusting PFT cover ratios of grid in the JULES model. Results show that NPP and LE flux were increased and SMC was decreased, especially during drought period. This was because multiple PFTs could better exploit ecosystem resources than the sole PFT does, which was related to differences in niche classified by phenology, WUE, and rooting depth.

The way the authors represented vegetation mixing was very interesting. Similar approach was done by Park et al. (2018)[^1] who varies tile size to represent land surface heterogeneity. I think these expriments are valuable because these are good examples that using ecosystem model to test ecological concept.

In addition to the design, they reasonably interpreted the beneath of the mixing effect. They caught difference in rooting depth between C3 plant and tree species and in phenology between deciduous trees and evergreen trees. Especially, I was impressed by the interpretation which related WUE to the different changes in magnitude by mixing between NPP and LE flux. By pointing out step by step in the timeseries considering WUE and other differences, the authors nicely described why the results came out.

[^1]: Park, J., Kim, H.-S., Lee, S.-J. and Ha, T. 2018. Numerical Evaluation of JULES Surface Tiling Scheme with High-Resolution Atmospheric Forcing and Land Cover Data. **_SOLA_**, 14, 19-24.