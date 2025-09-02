---
week: 6
session: 1
featured_image: assets/images/generalised-linear-models.png 
title: "Generalised Linear Models"
abstract:  >
layout: lecture
venue: LT2, William Gates Building
author:
- family: Lawrence
  given: Neil D.
  gscholar: r3SJcvoAAAAJ
  institute: University of Cambridge
  twitter: lawrennd
  url: http://inverseprobability.com
time: "10:00"
date: 2024-11-15
youtube: 1IM_t8miX6s
oldyoutube: 
- code: 1IM_t8miX6s
  year: 2024
- code: DgaZQcNp9fU
  year: 2022
- code: VQvYg3jin-k
  year: 2021
transition: None
reveal: true
ipynb: true
---


\include{_mlai/includes/mlai-notebook-setup.md}


\installcode{statsmodels}

\subsection{Review}

\notes{We introduced machine learning as a way to extract knowledge from data to make predictions through a prediction function and an objective function. We looked at a simple example of predicting whether someone would buy a jumper based on their age and latitude, *using logistic regression* to model the log-odds of purchase. This highlighted how machine learning can codify predictions through mathematical functions. This is an example of a broader approach known as *generalized linear models*.

When taking a probabilistic approach to supervised learning we're interested in predicting a class label, $\dataScalar_i$, given an input, $\inputVector_i$. That's represented probabilisticially as $p(\dataScalar_i|\inputVector_i)$. We can derive this conditional distribution through either (1) modelling the joint distribution, $p(\dataVector, \inputMatrix)$ and then dividing by the marginal distribution of the inputs, $p(\inputMatrix)$  , or (2) focusing specifically on modeling the conditional density, $p(\dataVector|\inputMatrix)$, that directly answers our prediction question. In the *generalised linear model* we choose the second approach. 

As we move to generalized linear models like logistic regression, we'll see how directly modeling the conditional density $p(\dataVector|\inputMatrix)$ can provide more flexibility in our modeling assumptions, while still allowing us to make the specific predictions we need.}

\include{_ml/includes/linear-regression-statsmodels.md}
\include{_ml/includes/logistic-regression.md}

\include{_ml/includes/logistic-regression-deployed.md}

\notes{\include{_ml/includes/olivetti-glasses-logistic.md}}
\include{_ml/includes/logistic-regression-going-further.md}
\include{_ml/includes/other-glms-statsmodels.md}

\include{_ml/includes/poisson-regression.md}
\include{_ml/includes/glm-practical-tips.md}

\reading

\thanks

\references


