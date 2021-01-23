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
