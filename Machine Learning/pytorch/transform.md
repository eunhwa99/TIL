## Transform
- 이미지 변형하기
---
PyTorch에서 image를 loading할 때, **torchvision.transform**을 사용할 수 있다.  
**transform**은 해당 image를 변환하여 module의 input으로 사용할 수 있게 변환해 준다.  
이때, 여러 단계로 변환해야 하는 경우 **transform.Compose**를 통해서 여러 단계를 묶을 수 있다.
```
train_transforms=transforms.Compose{[
    transforms.RandomHorizontalFlip(),
    transforms.RandomVerticalFlip(),
    transforms.Resize(500),
    transforms.CenterCrop(500),
    transforms.ToTensor(),
    transforms.Normalize(mean=[0.485,0.456,0.406],std=[0.229,0.224,0.225])
]}
```
1. RandomHorizontalFlip: 이미지를 랜덤으로 수평으로 뒤집는다. p=0이면 뒤집지 않는다.
2. RnadomVerticalFlip: 이미지를 랜덤으로 수직으로 뒤집는다. p=0이면 뒤집지 않는다.
3. Resize: 이미지 사이즈를 size로 변경한다.
4. CenterCrop: 가운데 부분을 size 크기로 자른다.
5. ToTensor: 이미지 데이터를 tensor로 바꿔준다.
6. Normalize: **ToTensor()이후에 사용해야 한다!** 이미지를 평균, 표준편차를 이용해 정규화한다. 여기서 사용한 mean, std의 파라미터 값은 ImageNet에서 사용한 값인데, 이 값을 이용하는 것이 관습이다. 
( _They are calculated based on millions of images.  
    If you want to train from scratch on your own dataset, you can calculate the new mean and std.   
     Otherwise, using the Imagenet pretrianed model with its own mean and std is recommended._
)  
의 순서로 PIL image를 tensor로 변경한다.  

### 함수 추가 설명
- transforms.ToPILImage() - csv 파일로 데이터셋을 받을 경우, PIL image로 바꿔준다.
- transforms.CenterCrop(size) - 가운데 부분을 size 크기로 자른다.
- transforms.Grayscale(num_output_channels=1) - grayscale로 변환한다.
- transforms.RandomAffine(degrees) - 랜덤으로 affine 변형을 한다.
- transforms.RandomCrop(size) -이미지를 랜덤으로 아무데나 잘라 size 크기로 출력한다.
- transforms.RandomResizedCrop(size) - 이미지 사이즈를 size로 변경한다
- transforms.Resize(size) - 이미지 사이즈를 size로 변경한다
- transforms.RandomRotation(degrees) 이미지를 랜덤으로 degrees 각도로 회전한다.
- transforms.RandomResizedCrop(size, scale=(0.08, 1.0), ratio=(0.75, 1.3333333333333333)) - 이미지를 랜덤으로 변형한다.
- transforms.RandomVerticalFlip(p=0.5) - 이미지를 랜덤으로 수직으로 뒤집는다. p =0이면 뒤집지 않는다.
- transforms.RandomHorizontalFlip(p=0.5) - 이미지를 랜덤으로 수평으로 뒤집는다.(글자 이미지를 데이터에 넣을 경우, 뒤집기 설정은 넣지 않는 것이 좋을듯?)
- transforms.ToTensor() - 이미지 데이터를 tensor로 바꿔준다.
- transforms.Normalize(mean, std, inplace=False) - 이미지를 정규화한다.

## Datasets
- 데이터셋 불러오기
```
torchvision.datasets.데이터셋 명( root,  train = True , transform = None, target_transform = None, download = False)
```

_데이터셋 종류_  
MNIST, Fashion-MNIST, KMNIST, EMNIST, QMNIST, FAKEDATA, COCO, LSUN, IMAGENET, CIFAR, SVHN 등

_파라미터_  
1. **root**: 데이터셋을 저장할 디렉토리 위치
2. **train**: 다운받을 데이터셋 종류(train/val/test) 
3. **download**-True할 경우, 인터넷에서 데이터셋을 root 경로에 다운받는다. 데이터가 있을 경우, 재다운하지 않는다.
4. **transform**-이미지를 변경한다.

위의 train_transforms는 아직 실제로 값을 변경하지는 않고, 이 transform 객체를 **dataset**에 연결해주면 dataset이 image를 loading할 때, 
이 transform 과정을 통해 tensor로 만들어 준다.
```
train_dataset = torchvision.datasets.ImageFolder(
    root=train_data_path,
    transform=transform_img
)
```
root에 image가 있는 directory의 path를 설정하고, transform에 위에서 설정한 transform을 할당한다.  
**ImageFoler**는 **DataLoader**가 data를 불러올 대상(root)와 방법(transform)을 정의하는 부분이라고 할 수 있다.  

## DataLoader
- 다운 받은 dataset은 DataLoader 함수를 이용해야 모델에 사용할 수 있다.
```
train_loader = torch.utils.data.DataLoader(
    train_dataset,
    batch_size=batch_size,
    num_workers=0,
    shuffle=True
)
```
DataLoader에 위 ImageFoler를 할당하고, 한 번에 불러올 batch_size를 지정한다.  
_파라미터_
1. **batch_size**: 모델을 한 번 학습시킬 때, 몇 개의 데이터를 넣을지 정한다. 1 배치가 끝날 때마다 파라미터를 조정한다.
2. **num_workers**: 몇 개의 subprocesses를 가동시킬것인지 정한다.
3. **drop_last**: 배치별로 묶고 남은 데이터를 버릴지(True) 여부를 정한다.

이제 이 DataLoader에서 batch_size만큼 image를 (transform으로 정의한 과정을 통해 tensor로 불러올 수 있다.)

