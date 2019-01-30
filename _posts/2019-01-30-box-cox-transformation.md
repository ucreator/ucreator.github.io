---
title: "Box-Cox Transformation"
date: 2019-01-30 22:10:00 +0900
categories: machine-learning
use_math: true
tags: [box-cox, yeo-johnson, power transform, gaussian, normal distribution, feature engineering]
---

Box-Cox Transformation

$x$ 가 정규분포가 아닌 경우 분포 자체를 적당히 변환시켜서 정규분포에 최대한 가깝게 만들어 준다.
정규분포가 왜 중요한가? 여러 통계 기법들이 확률 변수의 정규분포를 가정하고 있기 때문에 정규분포를 따르는 확룰 변수에는 적용할 방법들이 많아진다.
기계학습에서는 피쳐 분포가 골고루 퍼져 있어야 학습시키기 좋기 때문에 피쳐 분포가 정규분포에 최대한 가깝도록 변화한 후 학습시킨다.

많이 쓰이는 방법이 Box-Cox 변환이다.

$$ x'_\lambda = \frac{x^\lambda-1}{\lambda} $$

$\lambda$는 양수, 음수 모두 가능하며, $\lambda$가 0으로 가는 극한에서는 $$ x'_\lambda = \lim_{\lambda \to 0}\frac{x^\lambda-1}{\lambda} = \lim_{\lambda \to 0}\frac{x^\lambda \ln(x)}{1} = \ln(x) $$ 이 되어 변수 스케일 변환에 흔히 사용하는 로그 변환이다.

어떤 $\lambda$ 값이 정규분포에 가장 가깝게 변환시켜주는지 찾아야 한다.
scikit-learn의 preprocessing.PowerTransformer 함수는 maximum likelihood estimation 방법으로 이를 자동으로 찾아준다.


Box-Cox 변환을 위해서는 $x$가 양수이어야 한다.
이를 음수값이 포함된 데이터에도 적용할 수 있도록 확장하여 

$$ x'_{(\lambda_1, \lambda_2)} = \frac{(x+\lambda_2)^\lambda_1-1}{\lambda_1} $$
를 사용하기도 한다. 

$\lambda_2$ 는 음수인 최소값에 절대값을 씌운 값보다 크면 된다. 즉, 각 데이터에 더했을 때 모든 데이터를 양수로 만들 수 있는 수.

이를 더 일반화시킨 Yeo-Johnson transformation 은 아래와 같다.
$$
\begin{split}x_i^{(\lambda)} =
\begin{cases}
 [(x_i + 1)^\lambda - 1] / \lambda & \text{if } \lambda \neq 0, x_i \geq 0, \\[8pt]
\ln{(x_i) + 1} & \text{if } \lambda = 0, x_i \geq 0 \\[8pt]
-[(-x_i + 1)^{2 - \lambda} - 1] / (2 - \lambda) & \text{if } \lambda \neq 2, x_i < 0, \\[8pt]
 -\ln (- x_i + 1) & \text{if } \lambda = 2, x_i < 0
\end{cases}\end{split}
$$

- References
  - Box, George EP, and David R. Cox. "An analysis of transformations." [Journal of the Royal Statistical Society. Series B (Methodological) (1964): 211-252.](https://www.jstor.org/stable/2984418){:target="_blank"}
  - Yeo, In‐Kwon, and Richard A. Johnson. "A new family of power transformations to improve normality or symmetry." [Biometrika 87, no. 4 (2000): 954-959.](https://academic.oup.com/biomet/article-abstract/87/4/954/232908){:target="_blank"}
  - [box-cox-transformation]( https://www.statisticshowto.datasciencecentral.com/box-cox-transformation/){:target="_blank"} by Statistics How To
  - [Box-Cox Transformations](http://onlinestatbook.com/mobile/transformations/box-cox.html){:target="_blank"} by David Scott, onlinestatbook
  - [Power transform](https://en.wikipedia.org/wiki/Power_transform){:target="_blank"} in Wikipedia

- Python
  - [preprocessing.PowerTransformer](https://scikit-learn.org/stable/modules/preprocessing.html#preprocessing-transformer){:target="_blank"} in scikit-learn
  - [scipy.stats.boxcox](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.boxcox.html){:target="_blank"} by scipy

- R
  - [boxcox](https://www.rdocumentation.org/packages/MASS/versions/7.3-0/topics/boxcox){:target="_blank"} in MASS
  - [yeo.johnson](
https://www.rdocumentation.org/packages/VGAM/versions/1.0-6/topics/yeo.johnson){:target="_blank"} in VGAM
