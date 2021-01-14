---
title: "[PyTorch] How to use tensor"
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Machine-Learning
tags:
- PyTorch
- Tensor
toc: true
toc_sticky: true
toc_label: contents
---

## How to use tensor (feat. PyTorch)   


### Tensor Broadcasting   

같은 shape을 가진 tensor를 +, -연산을 시키는 데에는 어려움이 없을 것이다.
![image](https://user-images.githubusercontent.com/68745983/104286976-1fadb600-54f9-11eb-8517-38995a3f379d.png)

하지만 만약 다른 shape을 가진 tensor끼리 연산을 한다면 어떻게 될까?
![image](https://user-images.githubusercontent.com/68745983/104287758-3f91a980-54fa-11eb-859f-cc316df2100c.png)
(2, 2)의 크기의 tensor와 (1, 1)의 크기의 tensor를 합쳤더니 (1, 1)의 크기인 b가 (2, 2)로 확장이 되어 연산이 되었다.

![image](https://user-images.githubusercontent.com/68745983/104288300-f55cf800-54fa-11eb-9ca2-ddc839e572c1.png)
(1, 2)의 크기였던 b가 (2, 2)로 확장이 되어 연산이 되었다.

>**※주의점**   
>위와 같이 크기가 다른 tensor들이 확장이 되어 연산이 가능하다고 하더라도 해당 기능은 조심해서 사용해야할 필요가 있어 보인다.   
>우선, 예상치못한 결과 값을 가질 위험성이 높다.   
>더불어 위의 예시와 다르게 broadcasting이 불가능한 tensor shape들도 존재한다.   
>![image](https://user-images.githubusercontent.com/68745983/104288438-23423c80-54fb-11eb-9767-fffbc4899339.png)        



>**※[TIP] view(-1)?**   
> 우선 예제를 보고 설명을 해보자.
> ![image](https://user-images.githubusercontent.com/68745983/104310759-95287f00-5517-11eb-8b4e-269f46690688.png)
> 위에 주어진 초반의 a(이제부터는 a_befor이라고 하겠다.)의 shape는 (4, 2)이다.   
> view(-1, 4)를 시행시켰더니, (2, 4)로 shape이 변형되었다.   
> **view(-1, 4)는 4를 고정시키고 나머지는 내부 연산에 의해 정해라는 것이다.**   
> 즉, D1은 4로 정해진 2-tensor를 만드는 것이므로 내부 연산에 의해 주어진 a_before는 (2, 4)가 된 것이다.   



### Tensor Manipulation   

tensor를 조작하는 방법에 대해 알아보자.
#### 1. View   

*<span style="color:gray">Returns a new tensor with the same data as the self tensor but of a different shape.</span>*   
tensor기존의 data를 보존하고 shape를 변경하는 역할을 한다.   
**<span style="color:red">※변경되는 shape은 기존의 tensor내부의 원소 수와 호환가능해야 한다.</span>**
![image](https://user-images.githubusercontent.com/68745983/104292955-c3e72b00-5500-11eb-8e14-6cdcf81e7818.png)
주어진 tensor a를 view를 이용해 shape을 변경해보자.   

우선, a의 shape은 (2, 2)이므로 (1, 4)로 변경해보자.
![image](https://user-images.githubusercontent.com/68745983/104293262-2ccea300-5501-11eb-8bbc-1d5db34c55ac.png)
변경된 tensor a1이 의도대로 (1, 4)로 변경된 것을 알 수 있다.   

그렇다면 a를 (5, 2)로 변경한다면 어떻게 될까?
![image](https://user-images.githubusercontent.com/68745983/104293611-8767ff00-5501-11eb-91b8-18474b7e084f.png)
(5, 2)의 경우 5 * 2 = 10개의 원소를 포함하지만 기존의 a의 경우 2 * 2 = 4개의 원소를 포함하므로 호환이 되지 않는다.   
그러므로 reshape을 하는데 어려움이 있다.   

>(4, 2) shape의 tensor를 (2, 2, 2)로 변환시켜보자.
>![image](https://user-images.githubusercontent.com/68745983/104304425-b2a51b00-550e-11eb-945a-180d26ab4738.png)
>tensor의 원소가 배치된 순으로 shape이 변경된 것을 확인할 수 있다.

#### 2. Squeeze   

*<span style="color:gray">Returns a tensor with all the dimensions of input of size 1 removed.</span>*    
크기가 1인 차원을 삭제한다.   

1. 사이즈가 1인 차원이 하나 일때
	![image](https://user-images.githubusercontent.com/68745983/104307181-40363a00-5512-11eb-84e2-264b9e9ab302.png)
	shape가 (2, 1, 2)였던 Tensor가 (2, 2)로 reshape되었다.   

2. 사이즈가 1인 차원이 여러개 일때
	![image](https://user-images.githubusercontent.com/68745983/104309115-fbf86900-5514-11eb-85c9-277c9911009d.png)
    shape가 (2, 1, 1)이였던 Tensor가 (2)로 reshpe되었다.   
    
3. 사이즈가 1인 차원이 없을때
	![image](https://user-images.githubusercontent.com/68745983/104309495-9a84ca00-5515-11eb-8b77-c7d140772f27.png)
    shape가 변하지 않았다.
    
>**[TIP]**   
> 위의 squeeze예제를 보면  **a = a.squeeze()**와 같이 **<span style="color:red">out-place operation</span>**을 사용할 수 있으나,   
> **<span style="color:red">in-place operation</span>**을 사용할 수 있는 방법 또한 존재한다.
> ![image](https://user-images.githubusercontent.com/68745983/104310008-5fcf6180-5516-11eb-9299-be585108f8be.png)
> 위의 그림과 같이 연산 operation뒤에 _를 붙여주면 in-place operation이 가능하다.

#### 3. Unsqueeze   

*<span style="color:gray">Returns a new tensor with a dimension of size one inserted at the specified position.</span>*   
원하는 위치에 크기가 1인 차원을 추가한다.
![image](https://user-images.githubusercontent.com/68745983/104313614-9a87c880-551b-11eb-9fd9-99848b074e84.png)
인덱스가 1인 위치에 크기가 1인 차원을 추가하였다.   


#### 4. ones_like   

*<span style="color:gray">Returns a tensor filled with the scalar value 1, with the same size as input.</span>*   
input으로 제공된 tensor와 같은 size의 1로 이루어진 tensor를 반환한다.    
![image](https://user-images.githubusercontent.com/68745983/104314662-18000880-551d-11eb-9f4c-d962fedce179.png)   
size가 (2, 3)인 tensor를 매개변수로 전달하였더니 1만으로 이루어진 size가 (2, 3)인 tensor가 반환되었다.    

> **[TIP]**
> **ones**
> input으로 제공된 size와 동일한 사이즈의 1로만 이루어진 tensor를 반환한다.
> ![image](https://user-images.githubusercontent.com/68745983/104315113-cefc8400-551d-11eb-8eb7-8e55f6f5c2aa.png)  
> ※이와 비슷하게 zeros_like와 zeros가 존재한다.



### Reference
[02 Pytorch Basic_02.텐서 조작하기 1](https://wikidocs.net/52460)   
[02 Pytorch Basic_03.텐서 조작하기 2](https://wikidocs.net/52846)   
[PyTorch docs_torch.tensor](https://pytorch.org/docs/stable/tensors.html)    
[PyTorch docs torch](https://pytorch.org/docs/stable/torch.html)
