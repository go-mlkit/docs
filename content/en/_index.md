---
title: "go-mlkit documentation"
linkTitle: "Home"
type: docs
cascade:
  type: docs
description: "Machine learning in pure Go. Planned, wave 3 of the go-scikit roadmap."
---

**go-mlkit is the planned home of machine learning for go-scikit**: clustering, classification and model selection, the parts of MATLAB's Statistics and Machine Learning Toolbox and Mathematica's `FindClusters`, `Classify` and `Predict` that no go-scikit organisation covers. It is in **wave 3**, together with go-statistics time series (PLAN.md item 15).

**Status: planned (wave 3).** The organisation has no library and no
release tag. These pages state the scope, the plan and the references each
library will be validated against. The plan itself is
[PLAN.md](https://github.com/go-scikit/roadmap/blob/main/PLAN.md) of [go-scikit/roadmap](https://github.com/go-scikit/roadmap),
and the state of each item is in [STATUS.md](https://github.com/go-scikit/roadmap/blob/main/STATUS.md).

## Plan

In PLAN.md, wave 3:

- item 15 (wave 3): k-means, DBSCAN, Gaussian mixtures, trees and forests, SVM, cross-validation;
- later, priority 3: neural networks as `nn`, on top of the reverse mode of go-autodiff; this is deferred and not part of the first scope.

It builds on go-statistics, go-dataframe and go-ndarray; neural networks would also need go-autodiff.

## The libraries

| Library | Status | What it will provide |
| --- | --- | --- |
| [Machine learning]({{< relref "mlkit" >}}) | planned (wave 3) | Planned for wave 3: clustering, classification and model selection, validated against scikit-learn. |

Every library of the go-scikit family is pure Go (`CGO_ENABLED=0`), validated
against the tool that is the reference of its domain, run as an oracle from Go,
and measured against it on one core. None of that is claimed here yet: there is
nothing to measure.

## What each library's pages hold

| Library | Pages |
| --- | --- |
| Machine learning | [overview]({{< relref "mlkit" >}}) |

