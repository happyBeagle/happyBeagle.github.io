---
title: "[Pytorch] Basic of Logistic Regression"
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
toc: true
toc_sticky: true
toc_label: contents
---

## Basic of Logistic Regression 
    
우리는 실생활에서 O냐 X냐라는 문제를 가지고 고민을 할때가 많다. 즉, 두가지의 선택지를 두고 고민을 하는 문제가 많다. 이러한 문제를 **이진 분류(Binary Classification)**이라고 한다. 그렇다면 머신러닝에서는 어떻게 해당 문제를 해결할 수 있을 까?   

### 1. Binary Classification   
두가지의 선택지에서 하나를 선택해야하는 문제를 생각해보자. 나는 종양의 크기에 따른 음성, 양성 여부에 대해 생각해볼 것이다.   
![image](https://user-images.githubusercontent.com/68745983/105608303-9181db80-5de6-11eb-8fab-3618ce5a2a87.png)  
해당 그래프를 한번 보자. 우리가 기존에 배웠던 선형 회귀로 해당 문제를 풀고자 한다면, 꽤 복잡한 문제가 될 것이라 생각한다.  
1. 선으로 해당 경우를 나누기에는 정확도가 상당히 떨어질 우려가 있다. 
2. **분류를 할 수 있는 함수가 필요하다.**   

### 2. Logistic Regression  
로지스틱 회귀는 회귀 알고리즘이지만 주로 분류 작업에 많이 사용된다.  
#### Logistic Function   
우리는 로지스틱 회귀를 알아보기 위해 Sigmid함수에 대해 알아보자.   
![image](https://user-images.githubusercontent.com/68745983/105608708-f2f67a00-5de7-11eb-812c-e68705a3748a.png)
위의 함수를 그래프에 나타내 본다면,   
![image](https://user-images.githubusercontent.com/68745983/105608825-a95a5f00-5de8-11eb-9b74-df528763ac69.png)   

위와 같다. 즉, sigmoid함수는 항상 0 ~ 1 사이의 값을 가진다.   
그렇다면, 어떤 값(기준 값)을 토대로 기준값 이하는 X 기준값 이상은 O라고 할 수 있지 않을까?   

몰론 sigmoid함수도 W 즉, 가중치에 따라 경사도를 변경할 수 있고, bias값에 따라 좌, 우 이동이 가능하다.   
그렇다면 sigmoid함수로 어떻게 가설을 만들어 낼 수 있을 까?   
앞서 배운 선형 회귀를 활용하여 가설을 만들어 내자.   

즉, 선형회귀를 통해 얻은 예측값을 sigmoid함수에 넣는다면 구한 값을 통해 이진 분류가 가능해진다.   

![image](https://user-images.githubusercontent.com/68745983/105609158-b7a97a80-5dea-11eb-9f53-5615bb21931c.png)


#### Cost Function   
그렇다면 logistic regression에서는 cost를 어떻게 구할 까?   
우선, 이전에 사용하였던 평균 제곱 오차를 가져와서 생각해보자.   
![image](https://user-images.githubusercontent.com/68745983/105609302-b3ca2800-5deb-11eb-89a3-6ee69dda18e0.png)   
실제 값과 예측값(Y햇)의 차의 제곱의 평균으로 구하였다. 하지만 sigmoid 함수를 거친 값을 위와 같은 형식으로 cost를 구하려고 할 경우, 극솟값이 여러개가 생기게 된다. 즉 적합한 W와 b를 찾는 것이 아니라 Local minima에 빠질 수 있다는 것이다.   
그렇다면 우리는 이를 어떻게 해결해야 할까?   

앞서 계속해서 말해왔듯 우리는 sigmoid함수를 **이진 분류**를 하기 위해 사용한다. 그렇다면 분류의 값들을 0과 1이라고 하고 이를 유념하며 생각해보자.   
그렇다면, 답이 1일때 예측 값은 1애 가까울 수록 cost값이 줄어 들것이며, 답이 0일때 예측 값은 0에 가까울 수록 그 값이 줄어들어야한다.   
이를 충족하는 함수가 있을 까?   
**있다!! 우리는 <span style="color:red">log 함수</span>를 활용하면 된다.!!**   

![image](https://user-images.githubusercontent.com/68745983/105609480-fe986f80-5dec-11eb-961a-d09f616dc964.png)

이렇게 본다면 y값이 0일 때, 결과 값이 커질 수록 cost는 한없이 커질 것이며,   
y값이 1일때, 결과값이 작을 수록 cost는 한없이 커질 것이다.   

그렇다면 이를 하나의 수식으로 묶어 좀 더 계산에 용이하도록 해보자.

![image](https://user-images.githubusercontent.com/68745983/105609579-96965900-5ded-11eb-9579-516a32a55cd7.png)

우리는 logistic 회귀의 기본에 대해 배웠다 그러면 다음에는 직접 logistic회귀를 구현해보는 활동을 해보도록 하자.

###  Reference   
[04 로지스틱회귀_로지스틱회귀](https://wikidocs.net/57805)
