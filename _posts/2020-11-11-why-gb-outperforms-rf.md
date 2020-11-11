---
layout: post
title: Why Gradient Boosting <i>Almost</i> Always Outperforms Random Forest
description: 'TLDR: GB can reduce error via both bias and variance, RF can only reduce error by reducing variance'
comments: true
categories:
  - til
---
_TLDR: GB can reduce error via both bias and variance, RF can only reduce error by reducing variance_ \\
$$ \text{error} = \text{bias} + \text{variance} $$ \\
When building a Random Forest, we build a lot of _fully grown_ trees. Bias of the RF model equals to an individual tree hence the needs to build a fully grown tree with really low bias.
To reduce the overall error, we also reduce its variance by building a lot of trees.
With Gradient Boost, we build a lot of weak learners (small trees) and aggregate their results to reduce variance. And since we build a lot of these weak learners that improve upon previously built tree, we are also reducing its total bias.
