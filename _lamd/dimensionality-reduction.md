---
week: 5
session: 2
title: "Visualisation I: Latent Variable Modelling"
featured_image: slides/diagrams/dimred/dem_manifold_print002.png
layout: lecture
venue: LT2, William Gates Building
time: "10:00"
date: 2024-11-11
author:
- family: Lawrence
  given: Neil D.
  gscholar: r3SJcvoAAAAJ
  institute: University of Cambridge
  twitter: lawrennd
  url: http://inverseprobability.com
abstract: |
  In this lecture we turn to visualisation through latent variable modelling. Specifically, we introduce the idea of a latent variable model. Latent variable models are a probabilistic perspective on unsupervised learning which lead to dimensionality reduction algorithms. We will start by a review of regression from a probabilistic perspective and build on this to describe latent variable models.
youtube: 0mtK2_rc0IY
transition: None
ipynb: True
reveal: True
---

\include{_mlai/includes/mlai-notebook-setup.md}

\subsection{Review}

\include{_ml/includes/overdetermined-system.md}
\include{_ml/includes/underdetermined-system.md}
\include{_ml/includes/types-of-uncertainty.md}

\addreading{@Bishop:book06}{Section 1.2.3 (pg 21–24)}
\addreading{@Rogers:book11}{Sections 3.1-3.4 (pg 95-117)}
\addreading{@Bishop:book06}{Section 1.2.3 (pg 21–24)}
\addreading{@Bishop:book06}{Section 1.2.6 (start from just past eq 1.64 pg 30-32)}

\reading

\include{_ml/includes/clustering.md}
\include{_dimred/includes/high-dimensional-data.md}
\include{_dimred/includes/high-dimensional-effects.md}
\include{_dimred/includes/latent-variable-motivation.md}
\include{_dimred/includes/practical-dimensionality-reduction.md}
\include{_dimred/includes/dimensionality-reduction-failure-modes.md}
\include{_dimred/includes/high-dimensional-data-real.md}
\include{_dimred/includes/latent-variables.md}
\include{_dimred/includes/probabilistic-pca-model.md}
\include{_dimred/includes/probabilistic-pca.md}
\include{_dimred/includes/principal-component-analysis.md}


\include{_dimred/includes/osu-run1-ppca.md}
\include{_dimred/includes/robot-wireless-ppca.md}

\section{Interpretations of Principal Component Analysis}

\include{_dimred/includes/principal-component-analysis.md}
\include{_dimred/includes/pca-and-matrix-factorisation.md}
\include{_dimred/includes/pca-and-model-algorithm-separation.md}
\include{_dimred/includes/pca-effectiveness.md}

\section{Derivation of PPCA}

\include{_dimred/includes/ppca-marginal-likelihood.md}
\include{_dimred/includes/ppca-reconstruction.md}


\section{Multidimensional Scaling}

\include{_dimred/includes/mds-derivation.md}
\include{_dimred/includes/mds-pca-equivalence.md}

\include{_dimred/includes/iterative-dimensionality-reduction.md}
\include{_dimred/includes/local-vs-global-preservation.md}

\include{_dimred/includes/t-sne-intro.md}
\include{_dimred/includes/umap-intro.md}

\include{_dimred/includes/dimensionality-reduction-comparison.md}

\subsection{Summary and Key Points}

\notes{We've covered several key ideas about dimensionality reduction:

1. High-dimensional spaces have counter-intuitive properties:
   - The curse of dimensionality
   - Concentration of distances
   
2. Real data doesn't behave like random high-dimensional data because:
   - It lies near lower-dimensional manifolds
   - It has structure imposed by physics, biology, or other constraints
   
3. This structure makes dimensionality reduction possible:
   - PCA finds linear manifolds
   - More sophisticated methods can find nonlinear manifolds
   
4. The probabilistic perspective helps us:
   - Understand when methods will work
   - Quantify uncertainty in our reduced representations
   - Connect dimensionality reduction to other machine learning approaches}

\reading

\thanks

\references
