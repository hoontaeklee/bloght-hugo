---
title: "Paper Review: Zhang (2019). CLM4.5. JGRBG"
author: "Hoontaek Lee"
date: 2019-05-11T20:00:00+09:00
publishdate: 2020-03-01T16:30:00+09:00
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
- 2019
---

## 11 May, 2019 (Zhang, JGRBG, CLM4.5)

Zhang, L., Lei, H., Shen, H., Cong, Z., Yang, D. and Liu, T. (2019). Evaluating the representation of vegetation phenology in the Community Land model 4.5 in a temperate grassland. **_Journal of Geophysical Research: Biogeosciences_** 124.

This was a key paper for the first revision of my paper. This paper had its focus on improving phenology module in CLM 4.5 by comparing MODIS LAI. Two problem were issued and resolved. **First**, EOS in the CLM 4.5 was too late compared with that of MODIS LAI. The authors showed that too low threshold soil temperature for leaf offset caused this problem; the temperature was increased. **Second**, the model sometimes showed zero LAI during summer, which caused multiple growing cycles. This problem was resulted from too high rate of leaf onset. By adjusting the rate, this problem could be solved. And then the authors confirmed that how these improvements affected GPP and ET simulations at stand and national levels.

For me, it was impressive how the authors found the causes of the two problems. They thoroughly investigated the sensitivity of the model to some parameters relevant to the problems. And they analyzed the test results concerning the internal processes of the model. On top of that, the discussion about applicability of the modified model was well written. The authors classified temperate grassland and characterized them in terms of their phenology drivers. Based on the properties they judged which type of grassland the model can be applied to.   