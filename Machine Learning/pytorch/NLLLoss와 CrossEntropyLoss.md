## NLLLoss VS CrossEntropyLoss
---
둘다 cross-entropy 손실을 구하는 함수이고, 분류문제처럼 출력이 확률값일 때 사용된다.
- torch.nn.CrossEntropyLoss: LogSoftmax+NLLLoss가 함께 사용된다. 즉, CrossEntropyLoss는 SoftMax를 적용하고 손실값을 구하게 된다.
- 즉, CrossEntropyLoss를 적용한 모델은 모델 자체에 Softmax가 없을 것이고, NLLLoss만 적용한 모델은 모델 마지막 레이어에 Softmax가 있을 것이다.
1. CrossEntropyLoss가 적용된 모델
```
class CNN(nn.Module):
    def __init__(self):
        super(CNN, self).__init__()
        self.layer1 = nn.Sequential(
            nn.Conv2d(1, 32, (3, 3), padding=1, stride=(1, 1)),
            nn.ReLU(),
            nn.MaxPool2d((2, 2), padding=0, stride=2)
        )
        self.layer2 = nn.Sequential(
            nn.Conv2d(32, 64, (3, 3), padding=1, stride=(1, 1)),
            nn.ReLU(),
            nn.MaxPool2d((2, 2), padding=0, stride=(2, 2))
        )

        self.fc = nn.Linear(7 * 7 * 64, 10, bias=True)

        torch.nn.init.xavier_uniform_(self.fc.weight)
    def forward(self, x):
        x = self.layer1(x)
        x = self.layer2(x)
        x = x.view(x.shape[0], -1)
        x = self.fc(x)
        return x
```
- forward 코드를 보면, 선형 레이어를 거쳐 그대로 나온다.
2. NLLLoss가 적용된 모델
```
class Net(nn.Module):
   def __init__(self):
       super().__init__()
       self.conv1 = nn.Conv2d(1, 10, kernel_size=5)
       self.conv2 = nn.Conv2d(10, 20, kernel_size=5)
       self.conv2_drop = nn.Dropout2d()
       self.fc1 = nn.Linear(320, 50)
       self.fc2 = nn.Linear(50, 10)
   
   def forward(self, x):
       x = F.relu(F.max_pool2d(self.conv1(x), (2,2)))
       x = F.relu(F.max_pool2d(self.conv2_drop(self.conv2(x)), 2))
       x = x.view(-1, 320)
       x = F.relu(self.fc1(x))
       x = F.dropout(x, training=self.training)
       x = self.fc2(x)
       return F.log_softmax(x)
```
- 마지막 선형 레이어를 지나 softmax 함수가 적용된다.
