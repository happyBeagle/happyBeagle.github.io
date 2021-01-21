---
title: "[Pytorch]Practice of Linear Regression #3(feat. PyTorch)"
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Machine-Learning
tags:
- Machine-Learning_basic
- PyTorch
toc: true
toc_sticky: true
toc_label: contents
---

## Practice of Linear Regression #3(feat. PyTorch)   
    
그렇다면 이제 torch에서 지원해주는 모듈들을 사용해 선형회귀를 구현해보도록 하자.   
### 1.다중 선형회귀의 클래스를 만들어 학습하자.
#### 1.필요한 모듈을 import하자.   
![image](https://user-images.githubusercontent.com/68745983/105374900-88a8d280-5c4b-11eb-8486-a2909eb26cd9.png)   
* **import torch.nn as nn**   
	nn즉, neural networks의 약자이다. 현재 사용할 linear regression뿐만아니라, CNN, RNN등을 구현할때 많이 사용한다.   
* **import torch.nn.functional as F**   
	nn내부 함수들을 사용하기 위해 import하였다.  
    위에 nn을 import했음에도 그 내부의 모듈을 새로 import하는 것은 nn.functional.~~는 너무 길다...    
    
    
#### 2.Linear Regression Class를 구현하자.   
![image](https://user-images.githubusercontent.com/68745983/105375902-83985300-5c4c-11eb-9c0c-a2b5912f3be4.png)  
**우리는 다중 선형회귀 클래스를 구현한다.**   

* **self.linear = nn.Linear(input_dim, output_dim)**   
	- 선형회귀를 정의한다.
	- input_dim : 입력값의 크기를 정해준다.   
	- output_dim : 출력값의 크기를 정해준다.   
* **self.linear(data)**   
	- 내부에 저장된 parameter를 기반으로 data에 대한 예측값을 구해 낸다.   

#### 3.학습을 시켜보자.   
![image](https://user-images.githubusercontent.com/68745983/105377019-b42cbc80-5c4d-11eb-91ce-32cfe5582ffc.png)
* **model = MultiVariateLinearRegressionModel(feature_n, 1)**   
	- 다중 선형회귀 모델을 선언한다.  
* **optimizer = optim.SGD(model.parameters(), lr=1e-4)**   
	- 확률적 경사하강법의 최적화 방식을 사용하였다.   
    - 앞서 선언한 **model**에서 생성된 parameter를 초기 가중치로 넘겨주었다.   
    - 학습률(learning rate)를 0.0001로 정해주었다.  
* **hypothesis = model(x)**   
	- 주어진 training_data(위의 코드에서는 x)을 model을 통해 원하는 값을 예측하였다.   
* **cost = F.mse_loss(y, hypothsis)**  
	- 앞서 연산한 예측값과 해당 데이터에 대한 y즉, 정답값을 가지고 loss값을 구하였다.   
    - 해당 코드에서는 제곱 평균 값을 선택하였다.  

**결과 값을 확인하자.**  
![image](https://user-images.githubusercontent.com/68745983/105378112-d246ec80-5c4e-11eb-9c8b-fc4ec86340ac.png)   
cost값들이 점점 줄어드는 것을 확인할 수 있다.  
좀 더 편하게 보기 위해 이를 그래프로 표현해보면, 아래와 같다.   
![image](https://user-images.githubusercontent.com/68745983/105378245-fa365000-5c4e-11eb-980c-9b6049a57733.png)   


###  Reference   
[03 선형회귀_클래스로 파이토치 모델 구현하기](https://wikidocs.net/60036)   
[data set_house prices](https://www.kaggle.com/c/house-prices-advanced-regression-techniques)
