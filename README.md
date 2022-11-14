# seoul_house_price_prediction
# 서울시 아파트 별 변수를 독립변수
- 종속변수에 영향을 미치는 독립변수를 선정하는 과정이 어려움
--> 기존 논문을 근거로 독립변수 가져오기 

# 서울시 아파트 거래금액을 종속변수

#  rfind는 오른쪽부터 ' '가 몇 번쨰에 있는지 찾아주는 함수, 0 ,1, 2,3, 4, 순서로 count


- XGBRegressor (gbtree) 모델 
가격 예측 범위는 0 ~ 무한대의 특정 값이므로 regressor 생성
더 이상 rmse 값이 향상되지 않으면 중단
early_stopping_rounds 조기중단 조건을 설정, 5번의 반복하는 동안 성능 평가 지수를 최대치로 , 반복학습의 횟수
트리를 50000 개 생성
learning rate = 일반적으로 0.01 ~ 0.3 정도로 설정, learning rate가 높을수록 과적합 하기 쉽다.
n_estimators 는 가지의 수 학습의 수
의사결정기반모형(gbtree), 선형모형(gblinear), dart
n_estimators [ 기본값 : 100 ], 생성할 weak learner의 수, learning_rate가 낮을 땐, n_estimators를 높여야 과적합이 방지된다.
max_depth [ 기본값 : 6 ]트리의 maximum depth이다. 적절한 값이 제시되어야 하고 보통 3-10 사이 값이 적용된다. max_depth가 높을수록 모델의 복잡도가 커져 과적합 하기 쉽다.
reference
https://wooono.tistory.com/97


# MAE에 대한 정리
MAE(Mean Absolute Error) 평균 절대 오차
오차의 절대값을 모두 더해준 다음 size n개로 나누어주는 것 (제곱하지 않음)
MAE score가 낮을 수록 성능이 높음 , 다만 오차의 절댓값을 사용하기 때문에 실제값과 negative하게 차이나는지 positive 하게 차이나는지 구분 못함
1/n{sigma |xi-x}} x는 실제값 xi는 예측값
MSE는 손실함수로써 쓰이고 MAE는 회귀지표로써 사용된다



# cross_validation을 통해서 학습하기
train data로 학습을 진행하고 test set으로 검증할 때, 고정된 test set에 대해서만 잘 작동하는 과적합이 발생할 수 있음
따라서 전체 데이터 셋을 k개의 subset으로 나누고 test set을 중복없이 바꾸어가면서 평가를 진행
장점으로는 특정 test data set에 과적합을 방지하고, 정확도를 향상시킬 수 있고, 모든 데이터셋을 중복없이 사용하면서 데이터부족으로 인한 과소적합을 방지할 수 있다
단점으로는 반복횟수가 많기 때문에 시간이 오래걸린다

# Neural network model
0보다 작은 값이면 0을 반환하고, 0보다 큰 값이면 그 값을 그대로 output한다
0보다 큰 값일때 1을 출력하는 sigmoid와 다르다 relu
sigmoid는 binary classification에 적합한 신경망

- 신경망 예측이냐 분류냐에 따라 활성화함수가 달라짐
- 층을 몇 개로 둬야하는 지는 정해져있지 않고, accuracy나 MAE 보고 최적 layer 개수 찾기
https://medium.com/@kmkgabia/ml-sigmoid-%EB%8C%80%EC%8B%A0-relu-%EC%83%81%ED%99%A9%EC%97%90-%EB%A7%9E%EB%8A%94-%ED%99%9C%EC%84%B1%ED%99%94-%ED%95%A8%EC%88%98-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0-c65f620ad6fd
