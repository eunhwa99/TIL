# DeepLearning Study
- 딥러닝의 전반적인 것

## Linear Regression  
1. 수치형 설명변수 X와 연속형 숫자로 이루어진 종속변수 Y 간의 관계를 선형으로 가정하고, 이를 가장 잘 표현할 수 있는 회귀계수를 데이터로부터 추정하는 모델. 
2. Activation Function: Y=Wx+b  
3. Cost Function : MSE(오차 제곱합)  
 ex) 33명의 성인 여성에 대한 나이와 혈압 데이터를 가지고, 회귀계수를 구할 수 있고, 이를 통해 나이를 한 살 더 먹으면 혈압이 약 얼만큼 증가하는지 알 수 있다.  
4. 혈압이라는 연속형 숫자 대신, 범주형 변수를 이용한다면?
 ex) 나이와 암 발생여부(1이면 발생, 0이면 정상) 데이터가 주어졌을 때, 위와 동일한 방식으로 회귀모델을 구축하고 그래프로 그리면 이상한 모양이 나온다.  
5. 따라서, Y가 범주형(Categorical) 변수일 때는, 선형회귀 모델을 그래도 적용할 수 없다. 그래서 Logistic Regression이 탄생했다.

## Logistic Regression  
1. 실제 값과 비교하여, 예측 값과 실제 값이 가깝도록 학습하고, 새로운 값이 입력되면 그것을 분류하여 클래스에 속할 확률을 출력하는 학습 모델로, 데이터를 두 개 혹은 그 이상의 그룹으로 분류하는 문제에서는 로지스틱 회귀분석이 가장 기본적인 방법이다.   
2. Activation Function: Sigmoid, Softmax  
2-1) Sigmoid: 치역이 0과 1사이, Binary Classification 
2-2) Softmax: 확률의 합이 1이다, Multiple Classification  
3. Cost Function: BCE, CE  
3-1) BCE: Binary Cross Entropy (이항 분류)  
3-2) CE: Cross Entropy (다중 분류)

### Binary Classification
- 현재 딥러닝에서 분류에 대해 가장 흔히 사용되는 손실함수는 Cross Entropy Error (CEE) 이다.  

  ![image](https://user-images.githubusercontent.com/68810660/104878350-1c09ab80-599f-11eb-9bc5-fa6e96dd5f88.png)  
  t는 정답 값, y는 추론 값

- sigmoid: 이진분류에서 가장 많이 사용되는 활성화 함수
- softmax: 다중분류에서 가장 많이 사용되는 활성화 함수

- 이진분류를 CEE로 나타내면 L=-(tlog(y)+(1-t)log(1-y)), 참(1)/거짓(0)

## Overfitting
- gradient descent: 숙명적으로 학습시 overfitting이 발생한다.
- Overfitting을 최소화하자
1. 전체 observation에 대해서 특정 비율대로, training set, test set 그리고 validation set(검증세트)로 나누자.
- validation set: test set에서의 overfitting 방지 역할(우리는 training set에서 모델을 훈련하고, test set을 잘 통과하는 모델을 계속 찾아나가는 데, 이러한 일을 반복하다보면 training과 test set에 overfitting 된 모델이 만들어 질 수 있다.)
- training set으로 훈련을 하고, validation set으로 검증을 한 후에, test set에 대해서 test 하면 더 정확한 모델 얻을 수 있다.
- training set(0.8), validation set(0,0.1), test set(0.1, 0.2)

2. More Data, 데이터를 많이 모으자.
3. Less features, 특징을 적게 사용하자.
4. Regularization
- Early Stopping: Validation Loss가 더 이상 낮아지지 않을 때까지 학습하는 방법
- Reducing Network Size: nn의 사이즈를 줄여 학습할 수 있는 양을 줄이는 방법
- Weight Decay: Weight 파라미터의 크기를 줄이는 방법.
- Dropout
- Batch Normalization


## Gradient Vanishing/Exploding 문제
<해결법>
1. Change Activation function: sigmoid를 Relu로
2. Careful initialization: 초기화(Weight initialization) 
3. Small learning rate
4. Batch Normalization
- Internal Covariate Shift: 입력과 출력의 분포가 다른 것, 한 레이어마다 입력과 출력을 가지고 있는데, 레이어끼리의 Covariate Shift가 발생한다. 이를 해결하기 위해서, 각 레이어마다 normalization하는 레이어를 두어서 변형된 분포가 나오지 않게 하는 것으로, 미니 배치들마다 normalization 해 주는 것이다.
- Network의 각 층이나 Activation마다 input의 distribution이 달라지는 현상으로, 이를 막기 위해 간단하게 각 층의 input의 distribution을 평균 0, 표준편차 1인 input으로 normalize 시킨다. (각 mini-batch의 mean과 variance를 구하여 normalize한다.)
- Batch Normalization은 activation function 이전에 주로 사용한다.
