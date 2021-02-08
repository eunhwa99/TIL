## RNN: Recurrent Neural Networks

1.	RNN이 다른 신경망과 다른점
-	일반적인 신경망: Feed-forward neural networks(FFNets), FFNets에서는 데이터를 트레이닝 셋과 테스트 셋으로 나누어서 관리를 하고 트레이닝 셋을 통해서 신경망의 가중치를 학습시키고 이 결과를 테스트셋을 통해서 확인을 하는 방식
-	FFNets에서는 데이터를 입력하면 입력층에서 은닉층까지 연산이 차근차근 진행되고 출력이 나가게 된다. 이 과정에서 입력 데이터는 모든 노드를 딱 한 번씩만 지나가게 되는데 데이터가 노드를 한 번만 지나가게 된다는 것은 데이터의 순서 즉 시간적인 측면을 고려하지 않는 구조라는 의미이다. 즉, 데이터들의 시간 순서를 무시하고 현재 주어진 데이터를 통해서 독립적으로 학습을 하는 것이다.
-	RNN의 경우: 은닉층의 결과가 다시 같은 은닉층의 입력으로 들어가도록 연결되어 있다. 즉, 히든 노드가 방향을 가지고 엣지로 연결돼 순환구조를 이루는 (directed cycle) 인공신경망의 한 종류이다. **RNN이 순서 또는 시간이라는 측면을 고려할 수 있도록 해준다.**

2.	RNN 사용하는 곳
-	순서적인 측면을 고려해서 판단할 수 있다는 특성  Sequence data를 다룰 때 좋다. (ex. 문장, 유전자, 손글씨, 음성 신호, 센서가 감지한 데이터, 주가 등의 배열 혹은 시계열 데이터, 사진에 캡션을 달아주는 기능)

3.	RNN의 모습
 <img src="http://i.imgur.com/s8nYcww.png" width="500" height="350">
-	state ht는 직전 시점의 히든 state ht−1를 받아 갱신된다.
-	RNN은 기존 신경망과 비슷하게 순전파(forward propagation)과 역전파(backpropagation)을 수행해 parameter 값을 갱신해 나간다. 여기서, RNN이 학습하는 Parameter는 인풋 X를 히든레이어 h로 보내는 Wxh, 이전 히든레이어 h에서 다음 히든레이어 h로 보내는 Whh, 히든레이어 h에서 아웃풋 y로 보내는 Why
-	히든 state의 활성화함수는 tanh이다.

4.	RNN의 장점
-	입력이 어떤 길이를 가져도 프로세스 가능하다.
-	Historical 정보를 고려해서 연산한다.
-	Weight 들이 모든 시간에서 공유된다.

5.	RNN의 단점
-	연산이 느리다.
-	현재 state에서의 미래 입력에 대한 고려를 하지 않는다.
-	관련 정보와 그 정보를 사용하는 지점 사이의 거리가 멀 경우, 역전파시 그래디언트가 점차 줄어, 학습 능력이 크게 저하된다. (vanishing gradient problem)  

코드: <https://github.com/eunhwa99/NLP/blob/main/RNN.py>

## LSTM: Long Short-Term Memory

1.	LSTM이란
-	RNN의 히든 state에 **cell state**를 추가한 구조이다.
-	Cell state: 일종의 컨베이어 벨트 역할  state가 꽤 오래 경과하더라도 그래디언트가 비교적 잘 전파된다.

2.	LSTM의 모습
- 전체적인 모습  

  <img src="http://i.imgur.com/H9UoXdC.png" width="500" height="350">
  
 - Sigmoid Layer: 0 혹은 1의 값을 출력해서 각 구성요소가 영향을 주게 될지를 결정해준다.  
 
 <img src="https://mblogthumb-phinf.pstatic.net/MjAxODA3MDJfMTg1/MDAxNTMwNTM3NjA1NTkx.0DCPszGCOlYR_7A2ncUcc_5Pe39QnAQzjZPaqqHeyN4g.rhLsBGhweftTKuMwIENzByAxRwErcREem6OfjMicKUYg.PNG.magnking/image.png?type=w800" width="350" height="350">
 
 - Cell State를 보호하고 Control 하기 위한 3가지 Gate: Forget Gate Layer, Input Gate Layer, Tanh Layer  
 
 Step1: Cell State에서 어떤 정보를 버릴지 선택하는 과정  
 
 <img src="https://mblogthumb-phinf.pstatic.net/MjAxODA3MDJfNDIg/MDAxNTMwNTM3NjY2ODY1.wPgD2C5CFuiSBeQHGfW4r6vP3-8lcCwVlhva4Yv60-Ug.6W3-nvjwjOmxvpXDYNqETKS5NN1QejyVbbhfaDhcHRMg.PNG.magnking/image.png?type=w800" width="500" height="300"> 

**Forget gate**: ft는 ‘과거 정보를 잊기’를 위한 게이트, ht−1과 xt를 받아 시그모이드를 취해준 값이 바로 forget gate가 내보내는 값이 된다. Sigmoid 함수의 값이 0이라면 이전 상태의 정보는 잊고, 1이라면 이전 상태의 정보를 온전히 기억하게 된다.  

 Step2: 새로운 정보가 Cell State에 저장될지를 결정하는 단계  
 
 <img src="https://mblogthumb-phinf.pstatic.net/MjAxODA3MDJfMTE5/MDAxNTMwNTM3Njk2NDQ0.IHpHZkmHLEPEy6BBSawkJHOyXc4tmOgW4dxaoUZQ9Igg.Uds1bGjZouk5wL2vcc58-1RVV59tPphsG5PfV8o09iog.PNG.magnking/image.png?type=w800" width="500" height="300">
 
**Input gate**: it⊙gt는 ‘현재 정보를 기억하기’위한 게이트, ht−1과 xt를 받아 시그모이드를 취하고, 또 같은 입력으로 하이퍼볼릭탄젠트를 취해준 다음 Hadamard product 연산을 한 값이 바로 input gate가 내보내는 값이 된다. 
**Tanh layer**: Cell State에 더해질 수 있는 새로운 후보 값을 만들어 낸다.  

 Step3: 오래된 Cell State를 새로운 State로 업데이트  

<img src="https://mblogthumb-phinf.pstatic.net/MjAxODA3MDJfOTUg/MDAxNTMwNTM3ODE0ODYz.jt5zSaBb8oSvguFIsXkc0_OZuOZ_TdhR8eUHoZWAnasg.kR80qOlDeYCzT9lUOjho_cjlisJ6kSiSgocHBdPm5aUg.PNG.magnking/image.png?type=w800" width="500" height="300">
 
 Step4: 어떤 출력값을 출력할지 결정  
 
 <img src="https://mblogthumb-phinf.pstatic.net/MjAxODA3MDJfMjMw/MDAxNTMwNTM3ODQyMjYz.pw8dd1VqfN7ng48ofMHdxRJDl_QDF3A60GPlWzUnYcwg.tP5pjecFbfJGhxknEIUNfO-0L_HK5M7_aeYYYRd04jIg.PNG.magnking/image.png?type=w800" width="500" height="300">
 
참고 자료: 
<https://ratsgo.github.io/natural%20language%20processing/2017/03/09/rnnlstm/>
<https://m.blog.naver.com/PostView.nhn?blogId=magnking&logNo=221311273459&proxyReferer=https:%2F%2Fwww.google.com%2F>

