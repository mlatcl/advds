---
week: 5
session: 3
title: "Visualisation II: Modern Dimensionality Reduction"
layout: lecture
venue: LT2, William Gates Building
time: "10:00"
date: 2024-11-13
abstract: |
  Building on our understanding of discrete and continuous latent variables, this lecture explores modern approaches to dimensionality reduction. We examine the limitations of linear methods like PCA, introduce powerful nonlinear techniques like t-SNE and UMAP, and develop practical guidelines for choosing and implementing these methods. The lecture emphasizes the importance of understanding when methods preserve local versus global structure and how this affects their application.
transition: None
ipynb: True
reveal: True
---


\include{_mlai/includes/mlai-notebook-setup.md}

\section{Part 1: Linear PCA}

\include{_dimred/includes/principal-component-analysis.md}
\include{_dimred/includes/probabilistic-pca.md}
\include{_dimred/includes/mocap-ppca.md}

\section{Part 2: Beyond Linear Methods}
\include{_dimred/includes/dimensionality-reduction-failure-modes.md}
\include{_dimred/includes/local-vs-global-preservation.md}
\include{_dimred/includes/iterative-dimensionality-reduction.md}

\section{Part 3: UMAP and t-SNE}
\include{_dimred/includes/t-sne-intro.md}
\include{_dimred/includes/umap-intro.md}

\section{Part 4: Practical Implementation
\include{_dimred/includes/dimensionality-reduction-comparison.md}
\include{_dimred/includes/dimensionality-reduction-practical-tips.md}

\thanks

\references

<!--https://github.com/neelsoumya/visualization_lecture/blob/main/visualization_lecture.pptx

More material is in the repo:

https://github.com/neelsoumya/visualization_lecture/-->
