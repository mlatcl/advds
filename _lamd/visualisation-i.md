---
week: 5
session: 2
title: "Visualisation I: Discrete and Continuous Latent Variables"
featured_image: slides/diagrams/dimred/dem_manifold_print002.png
layout: lecture
venue: LT2, William Gates Building
time: "10:00"
date: 2024-11-11
abstract: |
  This lecture introduces different approaches to discovering latent structure in data. We begin by examining clustering as a discrete approach to finding latent structure, then explore why high dimensional data often has simpler underlying continuous representations. This motivates our introduction to Principal Component Analysis (PCA) as a fundamental approach to continuous latent variable modeling.
author:
- family: Lawrence
  given: Neil D.
  gscholar: r3SJcvoAAAAJ
  institute: University of Cambridge
  twitter: lawrennd
  url: http://inverseprobability.com
youtube: 0mtK2_rc0IY
transition: None
ipynb: True
reveal: True
---

\include{_mlai/includes/mlai-notebook-setup.md}

# Part 1: Discrete Latent Variables
\include{_ml/includes/clustering.md}

# Part 2: Continuous Latent Variables
\include{_dimred/includes/high-dimensional-data.md}
\include{_dimred/includes/high-dimensional-effects.md}
\include{_dimred/includes/high-dimensional-data-real.md}
\include{_dimred/includes/latent-variable-motivation.md}
\include{_dimred/includes/latent-variables.md}
\include{_dimred/includes/principal-component-analysis.md}
\include{_dimred/includes/probabilistic-pca.md}
\include{_dimred/includes/mocap-ppca.md}

\thanks

\references
