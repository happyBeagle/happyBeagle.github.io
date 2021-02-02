---
title: "[BoostCamp] DAY12 Deep Learning Basic#2"
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- BoostCamp_AI_Tech
tags:
- BoostCamp_AI_Tech
- AI_Basics
toc: true
toc_sticky: true
toc_label: contents
---

# [BoostCamp] DAY12 Deep Learning Basic#2
---   

## 1. Deep Learning Basics_Optimization   
### Optimization에서 중요한 컨셉    
#### - Generalization   
학습된 모델이 처음 보는 데이터에 대해 얼마나 잘 작동하는 가?   
![image](https://user-images.githubusercontent.com/68745983/106594130-07c7d000-6595-11eb-9197-9e89cf4287e4.png)    
#### - Underfitting VS Overfitting    
* **underfitting**: 학습 오류가 줄어 들지 않는 문제   
* **overfitting** : 학습 오류가 테스트 셋에 대한 오류보다 아주 작은 경우 나타나는 문제   
![image](https://user-images.githubusercontent.com/68745983/106594584-a81df480-6595-11eb-8220-30d3774eeaaa.png)    
> 출처 : https://www.geeksforgeeks.org/underfitting-and-overfitting-in-machine-learning/   

#### - Cross-Validation   
* 모델이 독립 데이터 세트로 일반화되는 방법을 평가하기 위한 모델 검증 기술이다.   

#### - Bias and Variance   
![image](https://user-images.githubusercontent.com/68745983/106596262-19f73d80-6598-11eb-9221-9c24a0af07fa.png)    
먼저, Cost에 대해서 고민해보자.   
![image](https://user-images.githubusercontent.com/68745983/106598042-91c66780-659a-11eb-9137-692c409ddcf3.png)   
** bias와 variance는 서로 반비례한다.**   

#### - Bootstrapping   
부트스트래핑은 가설 검증(test)을 하거나 메트릭(metric)을 계산하기 전에 random sampling을 적용하는 방법    

#### - Bagging VS Boosting   
* **Bagging (Bootstrapping Aggregating)**   
	* 다양한 모델들이 boostrapping으로 학습되는 것을 말한다.  
	* 기본 분류기는 개별 예측을 종합하는 임의의 subset에 맞춰진다.   

* **Boosting**   
	* 만약 분류하기 힘든 특정 트레이닝 샘플에 초점이 맞춰 진다면, 강력한 모델은 약한 모델들의 집하으로 이루어 질 수 있다.   

### 실험적인 경사하강법 방법들    
* **Stochastic Gradient Descent**   
	* 단일 샌플로 계산된 경사로 갱신한다.   
* **Mini-batch Gradient Descent**   
	* 데이터의 subset으로 계산된 경사를 갱신한다.     
* **Batch Gradient Descent**   
	* 모든 데이터로 계산된 경사를 갱신한다.   

#### - Batch-Size Matters   
![image](https://user-images.githubusercontent.com/68745983/106602065-d3a5dc80-659f-11eb-9638-26d6d8b619c3.png)    
mininum이 평평할 수록 약간의 오차가 생기더라도 Training과 Test의 차이가 적어진다.   

#### - Optimizer  종류   
##### Gradient Descent    
![image](https://user-images.githubusercontent.com/68745983/106607692-f5569200-65a6-11eb-87e5-87c8f5a015b5.png)    
새로운 **Weight**는 기존의 weight에서 해당 지점의 기울기를 Learning Rate와 곱하여 빼준다.   

##### Momentum   
기존의 **Gradient Descent**에서는 Overshooting의 문제(Learning Rate이 너무 크거나 데이터가 너무 가파른 곡선을 가지고 있어서 W값이 너무 큰 값으로 업데이트 되는 것)가 발생할 가능성이 있다. 이를 해결하기 위해 방향의 관성을 추가해주기 위해 **<span style="color:orange">Momentum</span>**이라는 개념을 추가하였다.    
![image](https://user-images.githubusercontent.com/68745983/106608678-094ec380-65a8-11eb-9cd9-54656859c18c.png)   
기존의 Learning Rate에 moementum을 곱하여 방향에 관성을 더 할 수 있도록 하였다.    

##### Nesterov Accelerated Gradient   
![image](https://user-images.githubusercontent.com/68745983/106608944-57fc5d80-65a8-11eb-8b22-87a162e440de.png)    
위의 식을 보자. 그럼 **Lookahead Gradient**가 어떤 것일까?   
![image](https://user-images.githubusercontent.com/68745983/106610444-25536480-65aa-11eb-90c8-94fb1f25282f.png)   
momentum벡터와 실제 W벡터 사이의 차를 새로운 gradient로 업데이트 한 후, 기존의 Gradient Descent처럼 연산을 하면 된다.    

##### Adagrad    
학습률이 너무 크면 overshooting, 너무 작으면 너무 느린 학습 때문에 문제가 생긴다. 이런 문제를 해결하기 위해 Adagrade는 학습률 감소라는 방법을 사용한다.    
![image](https://user-images.githubusercontent.com/68745983/106615901-461eb880-65b0-11eb-9ea7-d634665d4deb.png)    

##### Adadelta    
Adadelta는 Adagrad에서 분모값이 무작정 커지는 것을 방지하기 위해 gredient의 가중평균을 구해 더해 준다.    
![image](https://user-images.githubusercontent.com/68745983/106616743-3a7fc180-65b1-11eb-95a2-744fc06b9fb9.png)   

##### RMSprop   
Adadelta의 업데이트 단위를 맞춰주어 최적의 W값을 구하는 방법이다.   

##### Adam   
TODO   

### Reqularization    
1. Early Stopping    
2. Parameter norm penalty   
3. Data augmentation   
4. Noise robustness    
5. Label smoothing   
6. Dropout    
7. Batch normalization   


















## 2. CNN의 첫걸음    


## 3.TODO   
1. 2-2)의 논문 공부하기   
2. 나만의 dataset class구현해보기    
3. 최적화 알고리즘 하나씩 뜯어보며 공부하기     



## 4.그외 이모저모   
1. 강의  
- 오늘은 CNN과 Optimizer등에 대해 배웠다. 다양한 이렇게 많은 Optimizer들이 있다는 것을 알게 되었다. 각각 좀 더 심도있게 알아보며 학습하고 싶다.    
2. 피어 세션  
- 오늘 들었던 강의리뷰에서 각자 중점을 두고 본것이 다르다는 것에 놀랬다.
- 오늘 ResNet에 대해 학습을 하였는데, 코드를 보며 이해를 했다고 생각했으나 좀 더 공부가 필요하다는 것을 깨달았다. 더 열심히 해야겠다.    
- 오늘 조원분들이 EDA를 하는 것을 보았다. EDA를 시작해야하는 데 어떻게 해야할지 몰라 고민을 했는데 이제 조금은 알 수 있는 것 같다.
