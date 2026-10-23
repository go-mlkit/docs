---
title: "Machine learning"
weight: 10
description: "Planned for wave 3: clustering, classification and model selection, validated against scikit-learn."
---

<!-- From go-scikit/roadmap PLAN.md and its bib/ files: the text is the plan's, summarised, with links to the references. Change it there first. -->

**Status: planned, wave 3; repositories not created yet, one per algorithm family, names not fixed.**

Clustering, classification and model selection in pure Go (PLAN.md item 15, wave 3). The bibliography sizes the work as XL and proposes splitting it per algorithm, so the repository layout is not fixed.

No code exists yet: nothing on this page is released, measured or tested. It
says what the library is planned to provide and how it will be checked. The wave
and the order are in [PLAN.md](https://github.com/go-scikit/roadmap/blob/main/PLAN.md); the state of each item in
[STATUS.md](https://github.com/go-scikit/roadmap/blob/main/STATUS.md).

## What it will provide

| | |
|---|---|
| Clustering | k-means (Lloyd, k-means++ seeding), hierarchical clustering, DBSCAN, Gaussian mixtures by EM |
| Dimension reduction | PCA, factor analysis and rotations |
| Classification | logistic regression, SVM (SMO and dual coordinate descent), decision trees, random forests, gradient boosting, k-NN |
| Model selection | cross-validation splitters, grid search, metrics (accuracy, ARI and others) |
| Neural networks | deferred, priority 3: `nn` on top of go-autodiff's reverse mode, outside the first scope |

## References

The references the work starts from (bibliography first):

- [Lloyd, k-means, IEEE Trans. IT 28:129 (1982)](https://doi.org/10.1109/TIT.1982.1056489)
- Arthur and Vassilvitskii, k-means++, SODA 2007 (ISBN 978-0-89871-624-5)
- [Ester, Kriegel, Sander and Xu, DBSCAN, KDD 1996](https://www.aaai.org/Papers/KDD/1996/KDD96-037.pdf)
- [Cortes and Vapnik, support-vector networks, 1995](https://doi.org/10.1007/BF00994018)
- [Chang and Lin, LIBSVM, ACM TIST 2011](https://doi.org/10.1145/1961189.1961199)
- [Breiman, random forests, Machine Learning 45 (2001)](https://doi.org/10.1023/A:1010933404324)
- [Friedman, gradient boosting, Ann. Stat. 29:1189 (2001)](https://doi.org/10.1214/aos/1013203451)
- [Chen and Guestrin, XGBoost, KDD 2016](https://doi.org/10.1145/2939672.2939785)
- [Hastie, Tibshirani and Friedman, *The Elements of Statistical Learning*, 2nd ed.](https://doi.org/10.1007/978-0-387-84858-7)

## Reference implementations

| Implementation | Licence and use |
|---|---|
| scikit-learn (Python/Cython) | BSD-3-Clause; port permitted: k-means, DBSCAN, trees, forests, GMM |
| LIBSVM, LIBLINEAR (C/C++) | BSD-3-Clause; port permitted: SVM and logistic regression |
| malaschitz/randomForest (Go) | Apache-2.0; a reuse candidate |
| golearn (Go) | MIT; inspect only, last push 2024-01 |

## How it will be validated

Reference tools are run as oracles, driven from Go by exec with JSON on a pipe;
the unit suite must pass with no oracle installed.

| Oracle | How |
|---|---|
| scikit-learn, statsmodels | `uv run --with scikit-learn --with statsmodels`; JSON in, JSON out |
| UCI Machine Learning Repository | https://archive.ics.uci.edu (iris, wine, digits); per-dataset licences to check |

What "correct" means:

| Area | Criterion |
|---|---|
| Clustering and classification | deterministic given a seed: partitions exact against scikit-learn with the same initialisation; adjusted Rand index equal to 1 on a shared init |
| Accuracy | within cross-validation noise of the oracle |

## Risks and open questions

- Linear algebra is the bottleneck: PCA, SVM and GMM need QR, Cholesky and symmetric eigen solvers tested to LAPACK accuracy; check what go-ndarray and gonum provide before sizing.
- Corpus licences (UCI datasets) must be checked per file; prefer download-on-demand into a directory outside the repositories.
- The name `go-learn` is taken, so the organisation is go-mlkit.
