---
title: "Paper Review: Eller (2020). JULES-SOX. NPH"
author: "Hoontaek Lee"
date: 2020-02-22T20:00:00+09:00
publishdate: 2020-03-01T16:45:00+09:00
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

## 22 February, 2020 (Eller, NPH, JULES-SOX)

Eller, C.B., Rowland, L., Mencuccini, M., Rosas, T., Williams, K., Harper, A., Medlyn, B.E., Wagner, Y., Klein, T., Teodoro, G.S., Oliveira, R.S., Matos, I.S., Rosado, B.H.P., Fuchs, K., Wohlfahrt, G., Montagnani, L., Meir, P., Sitch, S. and Cox, P.M. (2020), Stomatal optimization based on xylem hydraulics (SOX) improves land surface model simulation of vegetation responses to climate. New Phytol. doi:[10.1111/nph.16419](https://doi.org/10.1111/nph.16419)



### Summary

Many researchers, including me, who use ecosystem models have recognized that the beta function approach for representing the change in plant photosynthesis to soil moisture stress needs improvement. In my case, I saw that the ET simulation by JULES was too sensitive to drought, resulting in underestimation. Eller et al. (2020) did a great work for developing an improved alternative method, especially considering xylem hydraulics. By a global evaluation for many biomes, the authors showed that the JULES-SOX outperformed the default JULES for most of evaluations. This improvement spreads out to more accurate estimates of global GPP and ET, predicting plant-physiological response mechanism under the drought condition, the demographic consequences resulted from the more competitive soil moisture use, and possibly replacing the PFT approach in LSMs and DGVMs to represent the large diversity of ecological strategies.



### SOX

**The main hypothesis of SOX** is "stomatal conductance is such as to maximize the product of leaf photosynthesis and xylem hydraulic conductance": maximize{A[ci(gs)] x K[psi(gs)]}

This approach successfully depicts stomatal responses to short- and long-term changes in environmental conditions (i.e., eCO2, soil moisture deficit, and so forth).

SOX estimates of gs is connected to the Collatz model to compute the leaf photosynthesis. 

Whereas, **JULES-default** computes ci using the Jacobs model, and then use the result to compute the leaf photosynthesis using the Collatz model.

Notably, the authors provided **the analytic solution** of the SOX, facilitating easier incorporation to other models and reducing the computing time.



### Other comments

The introduction greatly summarized the history of modelling stomatal conductance.  

CF (Cowan and Farquhar, 1977) - SPA (Williams et al., 1996) - Sperry (Sperry et al., 2017) - SOX (Eller et al., 2018)

CF: maximized A minus the carbon cost of water loss. But the cost of water loss is not linked to measurable variables.

SPA: incorporated plant hydraulics to constrain stomatal optimization, but still relied on a WUE optimization similar to CF.

Sperry: proposed a model that assumes that as xylem hydraulic conductance declines, **the increased risk of hydraulic failure is the main fitness cost** associated with low psi.

SOX: has a different optimization target from that of Sperry: stomata optimize plant dry matter production. In addition, SOX can be solved analytically.