## torch.topk
---
```
torch.topk(input, k, dim=None, largest=True, sorted=True, *, out=None) -> (Tensor, LongTensor)
```
- 주어진 input 텐서에서 주어진 dimension을 따라 K번째로 큰 요소를 반환한다. 
- dim이 주어지지 않으면, input의 마지막 dimension이 dim으로 할당된다. 
- largest가 False이면 k번째 작은 요소들이 반환된다.
- sorted가 True이면, 반환된 k개의 요소들끼리 정렬되어 있음을 보장한다.
- (values, indices)가 반환되며, indices는 input 텐서의 인덱스 값이다.  

<공식문서 예시>
```
>>> x = torch.arange(1., 6.)
>>> x
tensor([ 1.,  2.,  3.,  4.,  5.])
>>> torch.topk(x, 3)
torch.return_types.topk(values=tensor([5., 4., 3.]), indices=tensor([4, 3, 2]))
```
<Kaggle 예시>
```
 probs, classes = output.topk(1, dim=1)
```

## torch.max
---
```
torch.max(input) → Tensor
```
- input tensor의 최댓값 반환한다.
```
torch.max(input, dim, keepdim=False, *, out=None) -> (Tensor, LongTensor)
```
- (values, indices)를 반환한다. value는 주어진 dimension에서의 최댓값이고, indices는 최댓값을 가지는 텐서의 인덱스 값이다.
- keepdim=True이면, output tensor는 input tensor와 같은 사이즈를 가진다.
