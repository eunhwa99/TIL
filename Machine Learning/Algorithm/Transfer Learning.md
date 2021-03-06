 ## Transfer Learning (전이학습)

1.	Transfer Learning이란?
-	ImageNet과 같이 아주 큰 dataset에 훈련된 모델의 가중치를 가지고 와서 우리가 해결하고자 하는 과제에 맞게 재보정해서 사용하는 것
- 결과적으로, 비교적 적은 수의 데이터를 가지고도 우리가 원하는 과제를 해결할 수 있는 딥러닝 모델을 훈련시킬 수 있다.
-	Dataset가 유사한 분야에 학습된 Weight들을 전이하여 Fine-Tuning 기반 신경망 학습 재사용 기법

2.	왜 필요한가?
-	데이터 부족, 학습 시간 단축, 학습치 재사용

3.	전이학습의 주요 학습 기법
-	Fine-tuned ConvNet: 미리 학습된 ConvNet의 마지막 FC Layer만 변경해 분류 실행
-	Pre-trained Model: 미리 학습된 모델의 가중치를 새로운 모델에 적용
-	Domain Adaptation: 풍부한 데이터를 바탕으로 훈련 시, 도메인 구분 능력은 약하게 학습하여 Target Data를 분류가능하도록 모델 구축
-	Layer Re-use: 기존 모델의 일부 Layer를 재사용하여 부족한 Data domain 모델 구축에 활용

4.	Fine Tuning
-	 기존에 학습되어져 있는 모델을 기반으로 아키텍쳐를 새로운 목적(나의 이미지 데이터에 맞게) 변형하고 이미 학습된 모델 Weights로부터 학습을 업데이트 하는 방법으로 딥러닝에서는 이미 존재하는 모델에 추가 데이터를 투입하여 파라미터를 업데이트 하는 것을 말한다.
-	사전 학습된 모델을 이용하여 우리가 원하는 데이터에 미세조정, 즉 Fine Tuning으로 불리는 작은 변화만을 주어 학습시키는 방법을 “전이학습”이라고 한다.
-	Fine tuning은 “정교한”과 “파라미터”가 키 포인트이다. 밑에 예시 보기.  

참고 자료:  
 <https://haandol.github.io/2016/12/25/define-bottleneck-feature-and-fine-tuning.html>  
 <https://m.blog.naver.com/PostView.nhn?blogId=beyondlegend&logNo=221573349878&proxyReferer=https:%2F%2Fwww.google.com%2F>

<코드1>

```
# 모든 layer를 fine tuning ==> 시간은 조금 더 걸리지만 조금 더 정확하다.
model=models.resnet18(pretrained=True)
num_features=model.fc.in_features

model.fc=nn.Linear(num_features, 2) # 클래스 2개
model.to(device)

criterion=nn.CrossEntropyLoss()
optimizer=optim.SGD(model.parameters(), lr=0.001)

# sheduler: update learning rate
# every 7 epochs, lr is multiplied by gamma
step_lr_scheduler=lr_scheduler.StepLR(optimizer, step_size=7, gamma=0.1)
# for epoch in range(100):
 #   train() # optimizer.step()
 #   evaluate()
 #   scheduler.step()

model=train_model(model, criterion, optimizer, step_lr_scheduler, num_epochs=3)
```
<코드2>

```
# Freeze all the layers in the beginning ==> 시간은 조금 덜 걸리지만 조금 덜 정확하다.
model=models.resnet18(pretrained=True)
for param in model.parameters():
    param.requires_grad=False 

num_features=model.fc.in_features

model.fc=nn.Linear(num_features, 2) # 클래스 2개
model.to(device)

criterion=nn.CrossEntropyLoss()
optimizer=optim.SGD(model.parameters(), lr=0.001)

# sheduler: update learning rate

# every 7 epochs, lr is multiplied by gamma
step_lr_scheduler=lr_scheduler.StepLR(optimizer, step_size=7, gamma=0.1)
# for epoch in range(100):
 #   train() # optimizer.step()
 #   evaluate()
 #   scheduler.step()

model=train_model(model, criterion, optimizer, step_lr_scheduler, num_epochs=3)
```

  
  [전체 코드] (https://github.com/eunhwa99/NLP/blob/main/Transfer.py)
