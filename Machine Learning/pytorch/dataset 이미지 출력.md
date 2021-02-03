## PyTorch에서 특정 Dataset을 열어 이미지 출력하기

- Pytorch의 경우 ToTensor() 함수를 불러오면, 이미지가 자동으로 [0,1]의 값으로 변경된다. 
- 이를 화면에 출력하고자 한다면, 이 값을 다시 0부터 255 사이의 값으로 늘려야 해야 하지만, 다행히 파이썬의 matplotlib는 기본적으로 0부터 1사이의 값
이라고 해도, 알아서 인식하여 정상적인 이미지로 출력해준다. 하지만 별도로 OpenCV 등에서 활용하고자 한다면, 추가적인 전처리가 필요할 수도 있다.

- PyTorch는 기본적으로 이미지 데이터셋을 **[Batch Size, Channel, Width, Height]** 순서대로 저장하기 때문에, 이를 matplotlib로 출력하기 위해서는 각 이미지를 
**[Width, Height, Channel]** 형태로 변경해야 한다. 이는 numpy 라이브러리의 **transpose()** 함수를 이용해서 해결한다.

```
def custom_imshow(img): 
  img = img.numpy() 
  plt.imshow(np.transpose(img, (1, 2, 0))) 
  plt.show()
  
def process(): 
  for batch_idx, (inputs, targets) in enumerate(train_loader): 
    custom_imshow(inputs[0]) 
   
process()
```
혹은 iteration을 이용해서 DataLoader에서 한 배치씩 꺼낸다.
```
data_iter=iter(train_loader) # iteration --> 한 batch씩 꺼내어 확인
images, labels=data_iter.next()
custom_imshow(images[0])
```
