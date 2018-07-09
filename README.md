---
title: "Paired Randomization in R"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```
Paired matched design 
```{r}
library(nbpMatching)
# create a covariate matrix
binSamp = c(1,0)
df <- data.frame(id=LETTERS[1:26], val1=rnorm(26), val2=rnorm(26), val3 = sample(binSamp, 26, replace = TRUE))
df
# create distances
df.dist <- gendistance(df, idcol=1)
df.dist
# create distancematrix object
df.mdm <- distancematrix(df.dist)
df.mdm
# create matches
df.match <- nonbimatch(df.mdm, ndiscard = 0)
df.match$matches
# review quality of matches
df.qom <- qom(df.dist$cov, df.match$matches)
```
Try experiment may be simplier
```{r}
library(experiment)
binSamp = c(1,0)
df <- data.frame(id=LETTERS[1:25], val1=rnorm(25), val2=rnorm(25), val3 = sample(binSamp, 25, replace = TRUE))
df

testMatching = randomize(df, match = c(df$val1, df$val2, df$val3))
testMatching$treatment
```



