---
title: "[PyTorch] About Tensor"
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
toc: true
toc_sticky: true
toc_label: contents
tags:
- PyTorch
- Tensor
categories:
- Machine-Learning
---

## About Tensor (feat. PyTorch)

### Tensor?
텐서란 데이터의 배열이라고 생각할 수 있따. 그렇다면 tensor는 어떻게 표현이 될까?
#### Expression of Tensor   

| **Rank** | **Shape** | **Math Entity** | **Example** |
|:------:|:------:|:------:|:------:|
|    0    |   []     | Scalar | 28 |
|    1    |   [D0]     | vector | [0, 1, 2, 3] |
|    2    |   [D0, D1]     | matrix | [[1, 2], [3, 4]] |
|    3    |   [D0, D1, D2]     | 3-tensor | [[[1, 2], [3, 4]], [[5, 6], [7, 8]]] |
|...|...|...|...|
|   n | [D0, D1, D2,..., Dn- 1]| n-tensor| ....|


#### Type of Tensor   

| **Data Type** | **Pyton Type** |
|:------:|:------:|
| DT_FLOAT | torch.float32 |
| DT_DOUBLE | torch.float64 |
| DT_INT8 | torch.int8 |
| ... | ... |

참조 : [TORCH.TENSOR](https://pytorch.org/docs/stable/tensors.html)

### Numpy VS PyTorch

먼저 해당 라이브러리를 import해줍니다
![image](https://user-images.githubusercontent.com/68745983/104123467-ac883080-538e-11eb-9e9d-6188ac884c9e.png)

#### 1D tensor
![image](https://user-images.githubusercontent.com/68745983/104124544-cdec1b00-5394-11eb-8718-4176dfff9721.png)


>**note**
>tensor의 Rank 알아내기
>- numpy : tensor.ndim
>- PyTorch : tensor.dim()  
>
>tensor의 Shape 알아내기
>- numpy : tensor.shape
>- PyTorch : tensor.shape & tensor.size()


#### 2D tensor
![image](https://user-images.githubusercontent.com/68745983/104124579-f5db7e80-5394-11eb-9a68-8b1eec00601c.png)

### Reference
[02 Pytorch Basic_02.텐서 조작하기 1](https://wikidocs.net/52460)
