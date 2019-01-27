## Cross-Validation for Time-Series Modeling ##

### 데이터 쪼개기 ###

머신러닝 모델링을 할 때 데이터를 다음과 같이 세 부분으로 나누어 각기 다른 용도로 사용한다.
  * training data: 모형을 학습시키기 위하여 사용한다.
  * validation data: 모형의 하이퍼파라미터를 튜닝하기 위하여 사용한다.
  * test data: 학습시킨 모형을 새 데이터로 평가하기 위하여 사용한다.
  
어떻게 나눌 것인가? 데이터의 시간 순서가 중요한지 아닌지에 따라 다르다.
  * 데이터의 순서가 중요하지 않은 경우
    * 세 부분의 비율을 정하여 그 비율에 맞게 랜덤하게 할당하면 된다. 이 경우는 쉽다.
  * 데이터의 순서가 중요한 경우
    * 데이터의 선후 관계가 중요한 데이터(보통 시계열 데이터가 그렇다)에서는 시간상 인접한 데이터끼리 상관관계(auto-correlation 참고)가 높다. 여기서 문제가 발생한다.

시계열 데이터를 사용하여 모델링할 때 교차검증 위해 데이터를 어떻게 분할해야 하는지 알아보자.

### 참고문서 ###
  * [Time Series Nested Cross-Validation](https://towardsdatascience.com/time-series-nested-cross-validation-76adba623eb9) by Courtney Cochrane
  * [Cross-validation for time series](https://robjhyndman.com/hyndsight/tscv/) by Rob J Hyndman


