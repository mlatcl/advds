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

\include{_physics/includes/gauss-least-squares.md}
\include{_ml/includes/the-bayesian-approach.md}
\include{_ml/includes/bayesian-regression1d.md}
\include{_ml/includes/bayesian-1d-maths.md}

\subsection{The Joint Density}

* Really want to know the *joint* posterior density over the parameters $c$ *and* $m$.
* Could now integrate out over $m$, but it’s easier to consider the multivariate case.

\include{_ml/includes/two-d-gaussian.md}

\subsection{The Prior Density}

Let's assume that the prior density is given by a zero mean Gaussian, which is independent across each of the parameters, 
$$
\mappingVector \sim \gaussianSamp{\zerosVector}{\alpha \eye}
$$ 
In other words, we are assuming, for the prior, that each element of the parameters vector, $\mappingScalar_i$, was drawn from a Gaussian density as follows
$$
\mappingScalar_i \sim \gaussianSamp{0}{\alpha}
$$
Let's start by assigning the parameter of the prior distribution, which is the variance of the prior distribution, $\alpha$.

\code{# set prior variance on w
alpha = 4.
# set the order of the polynomial basis set
order = 5
# set the noise variance
sigma2 = 0.01}


\addreading{@Bishop:book06}{Multivariate Gaussians: Section 2.3 up to top of pg 85}
\addreading{@Bishop:book06}{Section 3.3 up to 159 (pg 152–159)}

\reading

\include{_ml/includes/clustering.md}
\include{_dimred/includes/high-dimensional-data.md}
\include{_dimred/includes/high-dimensional-effects.md}
\include{_dimred/includes/latent-variable-motivation.md}
\include{_dimred/includes/practical-dimensionality-reduction.md}
\include{_dimred/includes/dimensionality-reduction-failure-modes.md}
\include{_dimred/includes/high-dimensional-data-real.md}
\include{_dimred/includes/latent-variables.md}
\include{_dimred/includes/principal-component-analysis.md}

\include{_dimred/includes/probabilistic-pca.md}

\include{_dimred/includes/mocap-ppca.md}
\include{_dimred/includes/robot-wireless-ppca.md}
\include{_dimred/includes/ppca-interpretations.md}
\include{_dimred/includes/pca-in-practice.md}
\include{_dimred/includes/ppca-marginal-likelihood.md}
\include{_dimred/includes/ppca-reconstruction.md}
\include{_dimred/includes/mds-derivation.md}
\include{_dimred/includes/mds-pca-equivalence.md}

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
