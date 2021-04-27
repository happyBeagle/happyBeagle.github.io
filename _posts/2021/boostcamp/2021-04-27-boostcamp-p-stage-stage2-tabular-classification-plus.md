---
title: "[BoostCamp] P-stage stage2 Tabular  Classification Plus"
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- BoostCamp_AI_Tech
tags:
- Pstage_Tabular_Classification
toc: true
toc_sticky: true
toc_label: content
---

# [BoostCamp] P-stage stage2 정형 데이터 분류 Plus
---   

## 오늘의 목표

1. 정형데이터를 이미지로 만들어 CNN계열 모델 학습을 해보자.

## 1. 정형데이터를 이미지로 만든다고?

* 우리에게 주어진 데이터들은 생각보다 한정적이다.  
	* customer\_id, product\_id, description, price, quantity, total, country
* 이런 feature들 중 numeric한 요소들을 가지고 0~255값으로 scaling할 수 있지 않을까라는 의문이 들었다.
* 그렇다면 이미지로 학습이 가능하겠지?   
* 여기서 MNIST학습을 하는데서 착안하여 28 \* 28 크기의 이미지를 생성하여 학습을 한다면 어떨까라는 생각이 들었다.   
* 그렇다면 이미지를 어떻게 구성해볼까?   

### 1) 이미지를 생성해보자.   

* ![image](https://user-images.githubusercontent.com/68745983/116037018-7acb7900-a6a2-11eb-8d08-4ff0872bba34.png)   
* 먼저, 이미지를 생성할 때 위와 같이 생성하고자하였고, 하나의 그림은 한명의 customer의 구매 패턴을 나타내는 정보들을 넣고 싶었다.   
* 그래서 Row1 ~ Row28에 해당하는 요소로서 month정보를 의미하기로 하였다 [01, 02, 03, 04, 05, 06......]   
* 1 ~ 28은 해당하는 요소로서 각 month의 구매 비용의 합, 평균, min, max등의 값들을 나타내도록하였다.    
* ![image](https://user-images.githubusercontent.com/68745983/116115382-4df48180-a6f5-11eb-9986-9f394e2de941.png)   
* 위의 그림이 각 달의 정보를 넣은 각각의 customer\_id에 관한 image이다.   
* 0 즉, 지정한 달에 300이상의 금액을 사용하지 않은 경우의 image와 1 즉, 지정한달에 300이상의 금액을 사용한 경우의 image는 크게 차이는 나지 않지만 조금씩 차이가 나는 것을 볼 수 있다.   
* 이제 이렇게 만든 이미지를 가지고 학습을 시켜보자.    


## 2. 이미지 분류기   

* 그냥 토이로 재미로 하는 실습이기에 간단한 모델로만 돌려 볼것이다.   
* 실습한 내용   
* | model | pretrained |
|:--------:|:--------:|
|    ResNet18    |   True     |
|    ResNet18    |   False     |
|    ResNet50    |   True     |
|    ResNet50    |   False     |    

* 그러면 이제 각각의 실험 결과에 대해서 알아보고 마무리 짓는 것으로하자.
* 다만 testset의 결과 값을 알지 못하기에 validation set의 auc값으로 성능을 확인해봐야한다.   
* | dataset | data period|target month|
|:--------:|:--------:|:--------:|
|   train     | 2009.12 ~ 2010.11 | 2010.12|
| valid|2010.11 ~ 2011.10 | 2011.11|
|test|2010.12 ~ 2011.11 |2011.12|

### ResNet 18     

|ResNet18 (pretrained True)| ResNet18 (pretrained False) |
|:--------:|:--------:|
|![image](https://user-images.githubusercontent.com/68745983/116178466-955c2b80-a750-11eb-9fb8-94aae29dbd03.png)|![image](https://user-images.githubusercontent.com/68745983/116178578-c89eba80-a750-11eb-81d6-dadde153561a.png)|    

* pretrained 웨이트를 가지고 학습을 시켰을때 그 결과 값이 0.5이하의 성능을 보여주는 것을 보고 학습 시키는 image가 기존의 image들과 달라서 그 성능이 잘 나오지 않는 다는 것으로 생각하였다.    
* 하지만 ResNet50의 경우를 보았을 때 그 결과 값이 다르게 나와서 좀 더 고민을 하게 되었다.    

### ResNet 50      

|ResNet50 (pretrained True)| ResNet50 (pretrained False) |
|:--------:|:--------:|
|![image](https://user-images.githubusercontent.com/68745983/116178830-2c28e800-a751-11eb-9ec5-ec467ea2c5d2.png)|![image](https://user-images.githubusercontent.com/68745983/116178857-3814aa00-a751-11eb-8306-ac77d18b2f09.png)|    

* 이번엔 pretrained 웨이트를 썼을때 그 결과가 더 좋게 나온다는 것을 알 수 있었다.   
* 왜 그런지 알아 보고 싶다만, stage3도 시작되었기 때문에 다음에 시간이 될때 알아 보도록 해야겠다.    
* 그럼 20000~
