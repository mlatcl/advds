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
youtube: DgaZQcNp9fU
oldyoutube: 
- code: VQvYg3jin-k
  year: 2021
pdfslides: advanced-datascience-glm.pdf
transition: None
reveal: true
ipynb: true
---


\include{_mlai/includes/mlai-notebook-setup.md}

\installcode{statsmodels}

\subsection{Review}

\slides{}

\notes{We introduced machine learning as a way to extract knowledge from data to make predictions through a prediction function and an objective function. We looked at a simple example of predicting whether someone would buy a jumper based on their age and latitude, *using logistic regression* to model the log-odds of purchase. This highlighted how machine learning can codify predictions through mathematical functions. This is an example of a broader approach known as *generalized linear models*.

When taking a probabilistic approach to supervised learning we're interested in predicting a class label, $\dataScalar_i$, given an input, $\inputVector_i$. That's represented probabilisticially as $p(\dataScalar_i|\inputVector_i)$. We can derive this conditional distribution through either (1) modelling the joint distribution, $p(\dataVector, \inputMatrix)$ and then dividing by the marginal distribution of the inputs, $p(\inputMatrix)$  , or (2) focusing specifically on modeling the conditional density, $p(\dataVector|\inputMatrix)$, that directly answers our prediction question. In the *generalised linear model* we choose the second approach. 

As we move to generalized linear models like logistic regression, we'll see how directly modeling the conditional density $p(\dataVector|\inputMatrix)$ can provide more flexibility in our modeling assumptions, while still allowing us to make the specific predictions we need.}

\newslide{Linear Regression Reminder}

\notes{In linear regression, we model the relationship between a continuous response variable $\dataScalar_i$ and input variables $\inputVector_i$ through a linear function with Gaussian noise:

$$\dataScalar_i = \mappingFunction(\inputVector_i) + \noiseScalar_i$$

where $\mappingFunction(\inputVector_i) = \mappingVector^\top\inputVector_i = \sum_{j=1}^D \weightScalar_j\inputScalar_{i,j}$ and $\noiseScalar_i \sim \gaussianSamp{0}{\dataStd^2}$

This gives us a probabilistic model:

$$p(\dataScalar_i|\inputVector_i) = \gaussianDist{\mappingVector^\top\inputVector_i}{\dataStd^2}$$

The key components are:
- $\dataScalar_i$ is the target/response variable we want to predict
- $\inputVector_i$ contains the input features/explanatory variables  
- $\mappingVector$ contains the parameters/coefficients we learn
- $\noiseScalar_i$ represents random Gaussian noise with variance $\dataStd^2$

For the full dataset, we can write this in matrix form:

$$\dataVector = \inputMatrix\mappingVector + \noiseVector$$

where $\dataVector = [\dataScalar_1,\ldots,\dataScalar_N]^\top$, $\inputMatrix$ contains the input vectors as rows, and $\noiseVector \sim \gaussianSamp{\zerosVector}{\dataStd^2\eye}$.

The expected value of our prediction is:

$$\mathbb{E}[\dataScalar_i|\inputVector_i] = \mappingVector^\top\inputVector_i$$

This linear model forms the foundation for generalized linear models like logistic regression, where we'll adapt the model for classification by transforming the output through a non-linear function.}

\slides{* Linear regression models continuous response $\dataScalar_i$ vs inputs $\inputVector_i$:
  $$\dataScalar_i = \mappingFunction(\inputVector_i) + \noiseScalar_i$$
  where $\mappingFunction(\inputVector_i) = \mappingVector^\top\inputVector_i$ 
  
* Probabilistic model:
  $$p(\dataScalar_i|\inputVector_i) = \gaussianDist{\mappingVector^\top\inputVector_i}{\dataStd^2}$$

* Matrix form:
  $$\dataVector = \inputMatrix\mappingVector + \noiseVector$$
  
* Expected prediction:
  $$\mathbb{E}[\dataScalar_i|\inputVector_i] = \mappingVector^\top\inputVector_i$$
}

\setupcode{import statsmodels.api as sm
import pods}

\code{# Demo of linear regression using python statsmodels.
data = pods.datasets.olympic_marathon_men()
x = data['X']
y = data['Y']
# Add constant term to design matrix
x = sm.add_constant(x)
model = sm.OLS(y, x)
results = model.fit()
results.summary()
}

\slides{
* Model fit statistics help assess overall performance:
  * R-squared shows variance explained
  * F-statistic tests if model is useful
  * AIC/BIC help compare models

* Parameter estimates tell us about relationships:
  * Coefficients show effect direction/size
  * Standard errors show uncertainty
  * P-values test significance

* Residual diagnostics check assumptions:
  * Tests for normality and autocorrelation
  * Look for patterns that violate assumptions

* Visual inspection is crucial:
  * With 1D data we can plot everything
  * Helps spot patterns statistics might miss
  * Shows if relationship makes practical sense
}

\notes{The statsmodels summary provides several key diagnostic measures that help us evaluate our model fit and identify potential areas for improvement. Since we're working with one-dimensional data (year vs time), we can visualize everything easily to complement these statistical measures.

The model fit statistics show a moderately strong fit, with an R-squared of 0.744 indicating that our model explains 74.4% of the variance in the data. The adjusted R-squared of 0.733 confirms this isn't just due to overfitting. The very low F-statistic p-value (7.40e-09) confirms the model's overall significance. The AIC (10.08) and BIC (12.67) values will be useful when we compare this model against alternative specifications we might try.

Looking at the model parameters, we see a coefficient of -0.013 for our predictor, with a small standard error (0.002). The t-statistic of -8.515 and p-value of 0.000 indicate this effect is highly significant. The 95% confidence interval [-0.016, -0.010] gives us good confidence in our estimate. The negative coefficient confirms the expected downward trend in marathon times over the years.

However, the residual diagnostics suggest several potential issues we should investigate:

1. The Durbin-Watson statistic (1.110) indicates positive autocorrelation in the residuals, though not as severe as we might expect. This suggests we might want to:
   - Consider time series modeling approaches
   - Add polynomial terms to capture non-linear trends
   - Investigate if there are distinct "eras" in marathon times

2. The highly significant Jarque-Bera test (p-value 7.67e-12) tells us our residuals aren't normally distributed. The skew (1.929) and kurtosis (8.534) values show the distribution is strongly right-skewed with very heavy tails. We might want to:
   - Look for outliers or influential points
   - Consider robust regression techniques
   - Try transforming our response variable

3. The large condition number (1.08e+05) suggests potential numerical instability or multicollinearity issues. While less concerning with single-predictor models, we should:
   - Consider centering and scaling our predictor
   - Watch for numerical precision issues
   - Be cautious when extending to multiple predictors

The beauty of having one-dimensional data is that we can plot everything to visually confirm these statistical findings. A scatter plot with our fitted line will help us:
- Visually assess the linearity assumption
- Identify potential outliers
- Spot any systematic patterns in the residuals
- See if the relationship makes practical sense in terms of marathon performance over time

This visual inspection, combined with our statistical diagnostics, will guide our next steps in improving the model.}



\setupplotcode{import matplotlib.pyplot as plt
import mlai
from mlai import plot}

\plotcode{fig, ax = plt.subplots(figsize=mlai.plot.big_wide_figsize)
ax.plot(x[:, 1], y, '.')

# Plot the fitted line
ax.plot(x[:, 1], results.predict(x), '-')

ax.set_xlabel('Year')
ax.set_ylabel('Time')
ax.set_xlim(1890, 2030)
plt.show()
mlai.write_figure("linear-regression-olympic-marathon-men-statsmodels.svg", directory="\writeDiagramsDir/data-science")}

\notes{Looking at our plot and model diagnostics, we can now better understand the large condition number (1.08e+05) in our results. This high value likely stems from using raw year values (e.g., 1896, 1900, etc.) as our predictor variable. Such large numbers can lead to numerical instability in the computations.

To address this, we could consider:
- Centering the years around their mean
- Scaling the years to a smaller range (e.g., 0-1)
- Using years since the first Olympics (e.g., 0, 4, 8, etc.)

Any of these transformations would help reduce the condition number while preserving the underlying relationship in our data. The coefficients would change, but the fitted values and overall model quality would remain the same.}

\newslide{Linear Regression Fit}

\figure{\includediagram{\diagramsDir/data-science/linear-regression-olympic-marathon-men-statsmodels.svg}{80%}}{Linear regression fit to Olympic marathon men's times using `statsmodels`.}{linear-regression-olympic-marathon-men-statsmodels}

\notes{The plot reveals several key features that help explain our diagnostic statistics:

- The 1904 St. Louis Olympics appears as a clear outlier, contributing to the non-normal residuals (Jarque-Bera p=0.00432) and right-skewed distribution (skew=1.385)
- We can observe distinct regimes in the data:
  - Rapid improvement in times pre-WWI 
  - Disruption and variation during the war years
  - More steady, consistent progress post-WWII
- These regime changes help explain the strong positive autocorrelation (Durbin-Watson=0.242) in our residuals
- While our high R-squared (0.972) captures the overall downward trend, these features suggest we could improve the model by adding additional features:
  - Polynomial terms to capture non-linear trends
  - Indicator variables for different time periods
  - Interaction terms between features
  - Variables accounting for external factors like temperature or course conditions

To incorporate multiple features into our model, we need a systematic way to organize this additional information. This brings us to the concept of the design matrix.}

\slides{
* 1904 St. Louis Olympics: Major outlier
  * Explains non-normal residuals
  * Contributes to right skew
* Three distinct regimes visible:
  * Pre-WWI: Rapid improvement
  * War years: Disrupted progress
  * Post-WWII: Steady improvement
* Model improvements possible with extra features:
  * Polynomial terms
  * Period indicators
  * Interaction terms
  * External factors
}

\subsection{Design Matrix}

\slides{
* The design matrix $\designMatrix$ stores our features
* Each row represents one data point
* Each column represents one feature
* For $n$ data points and $p$ features:
  $$\designMatrix = \begin{bmatrix} 
  x_{11} & x_{12} & \cdots & x_{1p} \\
  x_{21} & x_{22} & \cdots & x_{2p} \\
  \vdots & \vdots & \ddots & \vdots \\
  x_{n1} & x_{n2} & \cdots & x_{np}
  \end{bmatrix}$$
* Also called the feature matrix or model matrix
}

\notes{The design matrix, often denoted as $\designMatrix$, is a key component of a statistical model. It organizes our feature data in a structured way that facilitates model fitting and analysis. Each row of the design matrix represents a single observation or data point, while each column represents a different feature or predictor variable.

For $n$ observations and $p$ features, the design matrix takes the form:

$$\designMatrix = \begin{bmatrix} 
x_{11} & x_{12} & \cdots & x_{1p} \\
x_{21} & x_{22} & \cdots & x_{2p} \\
\vdots & \vdots & \ddots & \vdots \\
x_{n1} & x_{n2} & \cdots & x_{np}
\end{bmatrix}$$

For example, if we're predicting house prices, each row might represent a different house, with columns for features like:

- Square footage
- Number of bedrooms  
- Year built
- Lot size

The design matrix provides a compact way to represent all our feature data and is used directly in model fitting. When we write our linear model as $\dataVector = \designMatrix\mappingVector + \noiseVector$, the design matrix $\designMatrix$ is multiplied by our parameter vector $\mappingVector$ to generate predictions.

The design matrix often includes a column of 1s to account for the intercept term in our model. This allows us to write the model in matrix form without explicitly separating out the intercept term.}


\setupcode{import statsmodels.api as sm
import pods
import numpy as np}

\code{# Demo of additional features with interactions regression usying python statsmodels.
data = pods.datasets.olympic_marathon_men()
x = data['X']
y = data['Y']

# Scale the year to avoid numerical issues
x_scaled = (x - 1900) / 100  # Center around 1900 and scale to century units

# Add to design matrix indicator variable for pre-1914
x_aug = np.hstack([x_scaled, (x[:, 0] < 1914).astype(np.float64)[:, np.newaxis]])

# Add to design matrix indicator variable for 1914-1945
x_aug = np.hstack([x_aug, ((x[:, 0] >= 1914) & (x[:, 0] <= 1945)).astype(np.float64)[:, np.newaxis]])

# Add to design matrix indicator variable for post-1945
x_aug = np.hstack([x_aug, (x[:, 0] > 1945).astype(np.float64)[:, np.newaxis]])

# Add product terms that multiply the scaled year and the indicator variables.
x_aug = np.hstack([x_aug, x_scaled[:, 0:1] * x_aug[:, 1:2], x_scaled[:, 0:1] * x_aug[:, 2:3]])[:, 0] * x_aug[:, 2]])

# Add constant term to design matrix
x_aug = sm.add_constant(x_aug)

# Do the linear fit
model = sm.OLS(y, x_aug)
results = model.fit()
results.summary()}


\setupplotcode{import matplotlib.pyplot as plt
import mlai
from mlai import plot}

\plotcode{fig, ax = plt.subplots(figsize=mlai.plot.big_wide_figsize)
ax.plot(x[:, 0], y, '.')

# Plot the fitted line
ax.plot(x[:, 0], results.predict(x_aug), '-')

ax.set_xlabel('Year')
ax.set_ylabel('Time')
ax.set_xlim(1890, 2030)
plt.show()
mlai.write_figure("linear-regression-olympic-marathon-men-augmented-statsmodels.svg", directory="\writeDiagramsDir/data-science")}

\newslide{Augmented Features with Interactions Regression Fit}

\figure{\includediagram{\diagramsDir/data-science/linear-regression-olympic-marathon-men-augmented-statsmodels.svg}{80%}}{Polynomial regression fit to Olympic marathon men's times using `statsmodels`.}{linear-regression-olympic-marathon-men-augmented-statsmodels}
The augmented model with interactions shows a significant improvement in fit compared to the simpler linear model, with an R-squared value of 0.870 (adjusted R-squared of 0.839). This indicates that about 87% of the variance in marathon times is explained by our model.

The model includes several key components:
- A base time trend (x1 coefficient: -0.6737)
- Indicator variables for different historical periods (pre-1914, 1914-1945, post-1945)
- Interaction terms between the time trend and these periods

The coefficients reveal interesting patterns:
- The pre-1914 period shows a significant positive effect (x2: 1.5506, p<0.001)
- The wartime period 1914-1945 also shows a positive effect (x3: 0.7982, p<0.05)
- The post-1945 period has a positive effect (x4: 0.6883, p<0.01)
- The interaction terms (x5, x6) suggest different rates of improvement in different periods, though these are less statistically significant

However, there are some concerns:
1. The very high condition number (2.79e+16) suggests serious multicollinearity issues
2. The Jarque-Bera test (p<0.001) indicates non-normal residuals
3. There's significant skewness (2.314) and kurtosis (10.325) in the residuals

Despite these statistical issues, the model captures the major trends in marathon times across different historical periods better than a simple linear regression would.

\include{_ml/includes/logistic-regression.md}


\newslide{Ad Matching for Facebook}

\slides{
* This approach used in many internet companies.
* Example: ad matching for Facebook.
  * Millions of advertisers
  * Billions of users
  * How do you choose who to show what?
* Logistic regression used in combination with [decision trees]()
* [Paper available here](http://www.herbrich.me/papers/adclicksfacebook.pdf)
}

\notes{Logistic regression is a widely used technique in many real world application domains. Within social media, the first wave of machine learning solutions were targeted at challenges such as ad matching or news-post ranking. In these domains the users are characterised by their previous behaviour (such as which posts they have liked) and other contextual information (such as which friends they have). The logistic regression approach is then used to predict which ads should be shown. For example Facebook's ad matching system faces the complex challenge of connecting millions of advertisers with billions of users. The scale of this matching problem is immense:

- Facebook has millions of potential advertisers, each with different target audiences and budgets
- There are billions of users, each with unique interests and behaviors
- Decisions about which ads to show must be made in real-time
- The system needs to balance between user experience and advertiser ROI

Facebook's solution employed a system that combines logistic regression with decision trees. The system considers various features including:

- User demographics and behaviour
- Historical ad performance
- Advertiser parameters and budgets
- Contextual information

The hybrid approach allows Facebook to make rapid predictions about ad performance while handling the massive scale of their platform. The details of this system are described in a [technical paper by Herbrich et al.](http://www.herbrich.me/papers/adclicksfacebook.pdf), which describes Facebook's click prediction system for online advertising, which combines decision trees with logistic regression to predict ad clicks. At the time Facebook had over 750 million daily active users and 1 million advertisers at the time. The authors found that a hybrid model outperformed either decision trees or logistic regression alone.}

\notes{Importantly, from our perspective, the researchers found that *feature selection* was the most critical factor - particularly choosing the features that capture historical information about users and ads. Given the 'right' features and model architecture, adapting the system to accommodate other aspects such as data freshness and learning rate tuning provided smaller incremental gains. To handle the scale of the task the system used a cascade of classifies to handle thecandidate ads per request efficiently. The hybrid model served as the final stage classifier. The paper also discusses practical considerations around implementing online learning and managing computational resources at scale.}

\notes{\include{_ml/includes/olivetti-glasses-logistic.md}}
\include{_ml/includes/logistic-regression-going-further.md}

\subsection{Other GLMs}

\slides{
* Logistic regression is part of a family known as *generalized linear models*
* They all take the form 
  $$g^{-1}(\mappingFunction_i(x)) = \mappingVector^\top \basisVector(\inputVector_i)$$
* Other examples include *Poisson regression*.}

\notes{We've introduced the formalism for generalized linear models. Have a think about how you might model count data using the [Poisson distribution](http://en.wikipedia.org/wiki/Poisson_distribution) and a log link function for the rate, $\lambda(\inputVector)$. If you want a data set you can try the `pods.datasets.google_trends()` for some count data.}

\include{_ml/includes/poisson-regression.md}
\include{_ml/includes/glm-practical-tips.md}


\reading

\thanks

\references


