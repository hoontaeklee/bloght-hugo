---
title: "Isolation Forest"
author: "Hoontaek Lee"
date: 2020-11-22T20:53:43+01:00
description:
draft: false
hideToc: false
enableToc: true
enableTocContent: false
tocPosition: outer
tocLevels: ["h2", "h3", "h4"]
tags:
- 2020
- R
- Research
---

```r
knitr::opts_chunk$set(eval = TRUE, 
                      echo = TRUE, 
                      warning = FALSE)
```

References: 

- solitude: https://github.com/talegari/solitude
- isofor: https://campus.datacamp.com/courses/anomaly-detection-in-r/isolation-forest

```r
# install.packages("mvoutlier"))
# install.packages("remotes"))
# remotes::install_github("Zelazny7/isofor")

#import libraries
library(ggplot2)
library(ggpubr)
library(solitude)  # hereafter, "sol"
library(isofor)  # hereafter, "iso"
library(viridis)
packageVersion("solitude")
```

```r
#create sample data
data("humus", package = "mvoutlier")

# 2-dimensional
columns_required <- c("Bi", "Cd")
humus2 <- humus[ , columns_required]

# multi-dimensional
columns_required_mul <- setdiff(colnames(humus)
                               , c("Cond", "ID", "XCOO", "YCOO", "LOI")
                               )
humus_mul <- humus[ , columns_required_mul]

str(humus2)
str(humus_mul)
```

```r
#plot data
ggplot(humus2, aes(x = Bi, y = Cd)) + 
  geom_point(shape = 1, alpha = 0.5) +
  labs(x = "Bi", y = "Cd") +
  labs(alpha = "", colour="Legend") +
  theme_bw()
```

```r
# solitude library

# sample (50%)
set.seed(1)
index <- sample(ceiling(nrow(humus2) * 0.5))
index_mul <- sample(ceiling(nrow(humus_mul) * 0.5))

# initiate an isolation forest
if_sol <- isolationForest$new(sample_size = length(index))
if_sol_mul <- isolationForest$new(sample_size = length(index))

# fit an isolation forest
if_sol$fit(humus2[index, ])
if_sol_mul$fit(humus_mul[index, ])
```

```r
# isofor library
if_iso <- iForest(humus2,
                  phi = nrow(humus2) * 0.5  # sample size
                  )
```

```r
# Obtain anomaly scores
humus2$score_sol <- if_sol$predict(humus2)$anomaly_score

humus_mul$score <- if_sol_mul$predict(humus_mul)$anomaly_score
humus2$score_iso <- predict(if_iso,
                            newdata = humus2[, c(1, 2)])

```

```r
# decision: outlier if score > 0.6 (threshold could vary by users)
humus2$is_outlier_sol <- ifelse(humus2$score_sol > 0.6, 1, 0)
humus2$is_outlier_iso <- ifelse(humus2$score_iso > 0.55, 1, 0)
```

```r
# create grid values for contour plot
Bi_seq <- seq(min(humus2$Bi),
              max(humus2$Bi),
              length.out = 100)
Cd_seq <- seq(min(humus2$Cd),
              max(humus2$Cd),
              length.out = 100)
humus2_grid <- expand.grid(Bi = Bi_seq,
                           Cd = Cd_seq)
humus2_grid$score_sol <- if_sol$predict(humus2_grid)$anomaly_score
humus2_grid$score_iso <- predict(if_iso,
                                 newdata = humus2_grid[, c(1, 2)])
```

```r
# scatter plot

sca_sol <-
  ggplot(humus2, aes(x = Bi, y = Cd, z = score_sol)) + 
  geom_point(aes(color = is_outlier_sol)) +
  labs(x = "Bi", y = "Cd") +
  scale_color_viridis(discrete = FALSE, 
                      direction = -1) +
  theme_bw()

sca_iso <-
  ggplot(humus2, aes(x = Bi, y = Cd, z = score_iso)) + 
  geom_point(aes(color = is_outlier_iso)) +
  labs(x = "Bi", y = "Cd") +
  scale_color_viridis(discrete = FALSE, 
                      direction = -1) +
  theme_bw()
```

```r
# contour plot
gmin <- min(humus2_grid$score_sol, humus2_grid$score_iso)
gmax <- max(humus2_grid$score_sol, humus2_grid$score_iso)
gbreaks <- round(seq(gmin, gmax, length.out = 9), 2)
  
cont_sol <-
  ggplot(humus2_grid, aes(x = Bi, y = Cd, z = score_sol)) + 
  geom_contour_filled(breaks = gbreaks) +
  
  labs(x = "Bi", y = "Cd") +
  theme_bw()

cont_iso <-
  ggplot(humus2_grid, aes(x = Bi, y = Cd, z = score_iso)) + 
  geom_contour_filled(breaks = gbreaks) +
  labs(x = "Bi", y = "Cd") +
  theme_bw()
```

```r
# aggregate ggplots
theme_set(
  theme_bw() +
    theme(legend.position = "top")
  )

if_plot <-
  ggarrange(sca_sol, sca_iso, 
            cont_sol, cont_iso,
            labels = rep(c("solitude", "iso"), 2),
            ncol = 2, nrow = 2)
if_plot
```

- Two scatter plots are similar even if they use different threshold values for the decision.
- Two contour plots look very different. This is because they have different range of scores. If we compare the regions with the same levels and colors, they show similar result.
