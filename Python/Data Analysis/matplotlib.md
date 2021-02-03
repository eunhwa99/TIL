## Pyplot
---
matplotlib.pyplot 모듈은 명령어 스타일로 동작하는 함수의 모음으로, pyplot 모듈의 함수를 이용해서 그래프를 만들고 변화를 줄 수 있다. 


## 기본 그래프
---
pyplot을 이용해서 값들을 간단하게 시각화할 수 있다.
```
import matplotlib.pyplot as plt

plt.plot([1, 2, 3, 4])
plt.ylabel('y-label')
plt.show()
```
pyplot.plot() 함수에 하나의 숫자 리스트를 입력함으로써 그래프가 르려진다. Matplotlob은 이 리스트의 값들이 y값이라고 가정하고, x 값 [0,1,2,3]을 
자동으로 만들어낸다. plot() 함수는 다양한 기능을 포함하고 있어서, 임의의 개수인 인자를 받을 수 있다.
```
plt.plot([1, 2, 3, 4], [1, 4, 9, 16])
```
이렇게 입력하면, 1,2,3,4가 x 값, 1,4,9,16이 y 값이 되어서 그래프가 그려진다.

## Magic 키워드
---
Juptyer Notebook은 사용자 편의를 위해 'Magic 키워드'를 지원한다.  
Magic 키워드는 **%** 또는 **%%** 를 이용하여 실행할 수 있다. 제공하는 기능은 여러가지가 있지만 주로 사용되는 것은 다음과 같다.
- 코드 실행시간 측정 - **%timeit**
- 그래프 등 시각데이터 출력 - **%matplotlib**

_%config InlineBackend.figure_format = 'retina' 를 %matplotlib 뒤에 넣어주면 그래프를 더 높은 해상도로 출력한다._

### %matplotlib inline
---
도표, 그림, 소리, 애니메이션과 같은 결과물들인 Rich Output을 나타내는 코드이다. 즉, 시각화하고 싶은 자료를 입력하면, jupyter notebook을 실행한 브라우저에 바로 그림을 나타낼 때 사용한다. jupyter notebook 실행시 주로 같이 사용하고 jupyter notebook을 실행한 브라우저에서 바로 그림을 볼 수 있게, 즉 브라우저 내부(inline)에 바로 그려지도록 해주는 코드이다.


