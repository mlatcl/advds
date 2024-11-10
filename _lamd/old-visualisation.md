---
week: 6
session: 1
title: "Visualisation"
featured_image: assets/images/visualisation.png
abstract: | 
  This lecture covers approaches to data visualization and
  dimensionality reduction, focusing on techniques like PCA, MDS and
  manifold learning. We explore both theoretical foundations and
  practical applications, from basic linear methods to advanced
  manifold learning approaches.
layout: lecture
venue: LT2, William Gates Building
author:
- family: Ek
  given: Carl Henrik
  gscholar: 9yQ1tQoAAAAJ
  institute: University of Cambridge
  url: https://carlhenrik.com/
- family: Lawrence
  given: Neil D.
  institute: University of Cambridge
  url: https://inverseprobability.com
time: "10:00"
date: 2024-11-15
youtube: hUI-nV0uyv4
oldyoutube:
- code: hUI-nV0uyv4
  year: 2021
#pdfslides: advanced-datascience-visualisation.pdf
#pdfworksheet: mds.pdf
transition: None
reveal: true
ipynb: true
---

<!-- Some visualisation dataset examples from Cornell: https://github.com/kuleshov/cornell-cs5785-2024-applied-ml/blob/main/slides/lecture11-mds-tsne.ipynb-->

\include{_visualization/includes/visualization-motivation.md}
\include{_data-science/includes/data-representation.md}

\notes{We begin with the mathematical foundations necessary for understanding dimensionality reduction.}

\include{_maths/includes/similarity-transform.md}
\include{_maths/includes/rank-nullity.md}
\include{_dimred/includes/manifold-definition.md}
\include{_maths/includes/inner-products-to-representations.md}

\notes{With these foundations established, we can derive our main approaches to dimensionality reduction.}

\include{_dimred/includes/mds-derivation.md}
\include{_dimred/includes/uk-cities.md}
\include{_dimred/includes/pca-probabilistic.md}
\include{_dimred/includes/mds-pca-equivalence.md}

\notes{We then explore how these methods can be extended to non-linear cases.}

\include{_dimred/includes/manifold-learning.md}
\include{_dimred/includes/nonlinear-extensions.md}


\notes{Finally, we consider practical aspects of working with high-dimensional data.}

\include{_dimred/includes/dimensionality-reduction-practical-tips.md}

\reading

\thanks

\references


1. Cox, M and T Cox (2008). "Multidimensional scaling". In: Handbook of data visualization.

2. Tenenbaum, Joshua B, Vin de Silva, and John C Langford (2000). "A Global Geometric Framework for Nonlinear Dimensionality Reduction". Science 290.5500, pp. 2319–2323.

3. Tipping, Michael E and Christopher M Bishop (1999). "Probabilistic principal component analysis". Journal of the Royal Statistical Society: Series B (Statistical Methodology) 61.3, pp. 611–622.
