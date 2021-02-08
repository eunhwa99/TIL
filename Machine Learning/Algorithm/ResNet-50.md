## ResNet-50
### ResNet 불러오기
---
- 50개 계층으로 구성된 Convolutional Neural Network로, ImageNet 데이터베이스의 1백만 개가 넘는 영상에 대해 훈련된 신경망의 사전 훈련된 버전을 
불러올 수 있다.
```
net=resnet50
net=resnet50('Weights','imagenet')

lgraph=resnet50('Weights','none')
```
- 위의 2개는 imageNet 데이터 세트에서 훈련된 ResNet-50 신경망을 반환
- lgraph는 훈련되지 않은 ResNet-50 신경망 아키텍처를 반환

### ResNet논문

**Introduction**
---
이전 연구들로 *모델의 layer가 너무 깊어질수록* *gradient vanihsing/exploding 문제* 때문에 학습이 잘 이루어지지 않아 성능이 오히려 떨어지는 현상이 발생했다. 
이를 극복하기 위해 ResNet이 고안되었다. ResNet은 skip connection을 이용한 residual learning을 통해 layer가 깊어짐에 따른 gradient vanishing 문제를 해결했다.

**ResNet**
---
![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbFPOry%2FbtqzR2En9ry%2F2DTETgT1BkCrW74hKQCsrk%2Fimg.png)
기존에는 input x가 네트워크를 통과해서 H(x)가 나오고, H(x)=y가 되도록 학습시켰다. 즉, 입력값 x를 타겟값 y로 매핑하는 함수 H(x)를 얻는 것이 목적이었다.
 하지만 **ResNet에서는 F(x)+x를 최소화하는 것을 목적으로 한다.** x는 현시점에서 변할 수 없는 값이므로, F(x)를 0으로 가깝게 만드는 것이 목적이 된다. 
 즉, input x가 네트워크를 통과한 값이 0이 되도록 하고, 여기에 x를 다시 더해서 H(x)=x가 되도록 학습시킨다. 이렇게 되면, 출력과 입력이 모두 x로 같아지게 된다. 
F(x)=H(x)-x이므로, F(x)를 최소로 해준다는 것은 H(x)-x를 최소로 해주는 것과 동일한 의미이고, H(x)-x를 **잔차(residual)**라고 한다. 즉, 잔차를 최소로 
해주는 것이므로 ResNet이란 이름이 붙게 된다.  
Q) residual 최소화시키기 위해서 F(x)=0이 되어야 하고, 즉 x=(x)가 되는 것인데, 이렇게 입력과 출력이 같아질수록 좋은 학습모델이라는 것인가?  
A) ResNet의 original 논문에 의하면, 경험적으로(empirically) 입력과 출력이 같아지도록 놓고 학습을 시켰더니 더 좋은 결과가 나왔다고 밝힘. 이것을 바탕으로 
여러 방식을 시도하고 변경해보다가 Residual 방식으로 학습하는 것이 좋은 성과를 본 것 같다.

1. 이미지에서 H(x)=x가 되도록 학습시킨다.
2. 네트워크의 output F(x)는 0이 되도록 학습시킨다.
3. F(x)+x=H(x)=x가 되도록 학습시키면 미분해도 F(x)+x의 미분값은 F'(x)+1로 최소 1이상이다.
4. 모든 layer에서의 gradient가 1+F(x)이므로 gradient vanishing 현상을 해결했다.

**ResNet의 구조**
---
기본적으로 VGG-19의 구조를 뼈대로 하고, 여기에 Convolution 층들을 추가해서 깊게 만든 후에, shortcut들을 추가한다.
![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbdQ7nn%2FbtqzVCKyKVV%2F5nkGhNvCqK9BcIgasYRxH0%2Fimg.jpg)
- 34층의 ResNet은 처음을 제외하고 균일하게 3X3 사이즈의 Convolution Filter를 사용했다. Feature Map의 사이즈가 반으로 줄어들 때, Feature Map의 Depth(채널 수)는 2배로 높였다.  

**ResNet의 성능**
---
plain 네트워크와 ResNet의 성능 비교
![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcgRYEe%2FbtqzR2j5F2f%2Fys3CXq3F7Y4Q2PaYEFfN80%2Fimg.png)
- 왼쪽 그래프에서 plain 네트워크는 망이 깊어지면서 오히려 에러가 커졌다. 오른족 그래프에서 ResNet은 망이 깊어지면서 에러도 작아졌다.  

아래 표는 18층, 34층, 50층, 101층, 152층의 ResNet이 어떻게 구성되어 있는지를 보여준다. 152층의 ResNet이 가장 성능이 뛰어나다.
  
![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FzwdXd%2FbtqzVoeJwoE%2F9oMcs2Qkj5m07pKPHRmeK0%2Fimg.png)

참고: <https://bskyvision.com/644>  
<https://ganghee-lee.tistory.com/41>
  
  
