---
title: "Dice"
author: "Jon Powell"
date: "18/07/2020"
output: github_document
editor_options: 
  chunk_output_type: console
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

First install some packages. It may be worth creating a source, script, with frequently used packages in the future but until that time manually install what you need first

```{r, include=FALSE}
library(tidyverse)
library(here)

```

Creating a dice starting with a vector of numbers (1:6)

```{r}
die <- 1:6

#standard element-wise mulitplcation (this means shorter vectors will be recyled in order to produce results if vectors are of uneven lengths)
die * die

#For traditional matrix based inner multiplicaiton use "%*%"
die %*% die

#For traditional matrix based outer multiplication use "%o%"
die %o% die

```

First a little bit about functions
If in doubt use args(function) to see what the arguments in a given function are i.e. args(round)

```{r}
# sample twice from the vector die but is there replacement? NO!
sample(x = die, size = 2)

args(sample)

sample(x = die, size = 2, replace = TRUE)

roll <- function(){
  die <- 1:6
  dice <- sample(die, size = 2, replace = TRUE)
  sum(dice)
}

roll2 <- function(bones = 1:6){
  dice <- sample(bones, size = 2, replace = TRUE)
  sum(dice)
  
}

```

The project creates at set of wieghted dice
```{r}

replicate(10, roll())

rolls <- replicate(10000, roll())
qplot(rolls, binwidth = 1)

reroll <- function(m = 1:6){
  dice <- sample(m, size = 2, replace = TRUE,
                 prob = c(1/8, 1/8, 1/8, 1/8, 1/8, 3/8))
  sum(dice)
}

rerolls <-  replicate(10000, reroll())
qplot(rerolls, binwidth = 1)

```

