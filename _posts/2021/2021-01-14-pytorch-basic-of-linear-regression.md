---
title: "[Pytorch] Basic of Linear Regression"
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
toc: true
toc_sticky: true
toc_label: contents
categories:
- Machine-Learning
tags:
- Machine-Learning_basic
- PyTorch
---

## Basic of Linear Regression (feat. PyTorch)   


### Regression?
주어진 data를 기반으로 **연속된 결과 값**을 도출해내는 과정을 일컫는다.

*example*    
- 학습시간이 feature으로 주어지고 시험 점수를 예측하는 문제
- 방의 수, 위치, 집이 지어진 년도 등이 feature으로 주어지고 집값을 예측하는 문제

>※feature?    
>학습을 할 때, 학습을 하는데 사용되는 데이터를 **feature**라고 한다.   
>학습을 하는 feature를 기반한 값을 **label**이라고 한다.   
>만약 학습시간을 통한 시험 점수를 예측하는 문제를 풀어본다고 생각해보자.   
>이때 학습시간은 **feature**이다.   
>또한, 여기서 시험 점수는 **lebel**이 된다.


### Linear Regression?
주어진 feature를 선형 방정식의 기반으로 값을 예측한다.

#### 1.Hypothesis
![image](https://user-images.githubusercontent.com/68745983/104453378-aa6cde80-55e7-11eb-893c-d0422558cc32.png)
**linear regression**은 선형 모델을 가진다.  
즉, feature 값을 x라고 했을 때, 모델을 통해 예측한 결과는 H(X)가 되는 것이다.   

* W : weight   
* b : bias  

 >학습시간에 따른 시험 점수 예측을 해보자.
 > ![image](https://user-images.githubusercontent.com/68745983/104598935-80d0b780-56ba-11eb-8c16-285c512e018a.png)
> 주어진 표에서 w = 0.5, b = 0인 경우를 생각해보면   
> 0.5 \* 1 + 0 = 0.5  
> ....   
> 등의 결과를 가질 수 있다. 그렇다면,   
>  <span style="color:red">**해당 모델의 정확성은 어떻게 판단 할 수 있을까?**</span>

#### 2.Cost Function
앞선 Hypothesis세션에서 우리는 선형회귀(Linear Regression)모델에 대해 배웠다.   
그렇다면 우리는 어떻게 모델을 평가할까?  
*※이제부터 Y는 실측 값이며 ^Y(y햇)은 예측값이라고 하자.*   

먼저, **Y - ^Y**로 모델의 정확도를 계산한다고 가정하자.    
그렇다면 Hypothesis세션에서 나온 예제를 생각해보자.
> ![image](https://user-images.githubusercontent.com/68745983/104598935-80d0b780-56ba-11eb-8c16-285c512e018a.png)
> 주어진 표에서 w = 2, b = -2인 경우를 생각해보면   
> ^Y¹ = 2 \* 1 - 2 = 0   
> ^Y² = 2 \* 2 - 2 = 2   
> ^Y³ = 2 \* 3 - 2 = 4   
> 즉, ∑(^Y - Y)를 계산해 본다면  (0 - 1) + (2 - 2) + (4 - 3) = 0이 된다.  

위의 주어진 예제에서 보듯, 예측값과 실측값의 차를 바로 합해서 계산한다면   
**제대로된 모델의 평가를 진행할 수 없음을 알 수 있다.**   
이를 해결하기 위해 각각의 값들을 <span style="color:red">**제곱**</span>하여 더해보자.  
![image](https://user-images.githubusercontent.com/68745983/104591733-73aecb00-56b0-11eb-8b2a-e27faf2fc330.png)
 * H(x^i) : i번째 feature를 넣었을 때 예측 값   
 * Y^i    : i번째 label   
 * n      : data의 갯수   
 * w      : weight   


>![image](https://user-images.githubusercontent.com/68745983/104598935-80d0b780-56ba-11eb-8c16-285c512e018a.png)
> 주어진 표에서 w = 2, b = -2인 경우를 생각해보면   
> 즉, ∑(^Y - Y)를 계산해 본다면    
>  (0 - 1)^2 + (2 - 2)^2 + (4 - 3)^2 = 2가 된다.  


<span style="color:hotpink">※Cost Function = Loss Function = Error Function = Objective Function</span>   
이제 cost(x)의 값을 줄이는 방법에 대해 생각해볼 필요가 느껴진다.   

#### 3.Optimize   
이제 Cost값을 줄이는 방법에 대해 고민해보자.   
![image](https://user-images.githubusercontent.com/68745983/104594529-9fcc4b00-56b4-11eb-88eb-72d0f81e5802.png)   
Linear Regression에서 Cost Function의 값은 2차 방정식이므로 위와 같이 그래프를 그릴 수 있다.   
이때, 우리는 최소 cost값을 찾기위해서 극솟값을 찾아내야한다.   
그렇다면 어떻게 극솟값을 찾아낼 수 있을 까?   
##### 1) Gradient Descent   
![image](https://user-images.githubusercontent.com/68745983/104595755-6268bd00-56b6-11eb-8f1a-bab79c789e16.png)   
위와 같이 특정 W값에서 시작해 극솟값을 찾아가면 된다.
그렇다면, 현재 W의 값이 극솟값이라는 것은 어떻게 알 수 있을까?   
**<span style="color:red">미분을 이용하자.</span>**
![image](https://user-images.githubusercontent.com/68745983/104596921-03a44300-56b8-11eb-95ab-f05680cdfbe8.png)   
* 기울기가 양수일 때, W값을 감소 시킨다.   
* 기울기가 음수일 때, W값을 증가 시킨다.   
>※ α란?   
>learning rate라고 한다. W값을 변화시킬 때, 그 비율을 정해주는 역할을 한다.    
>* α가 매우 클 때, W값이 발산할 위험이 있다.   
>![image](https://user-images.githubusercontent.com/68745983/104597764-1408ed80-56b9-11eb-8026-ca24b00fbe02.png)
>* α가 매우 작을 때,학습 속도가 매우 느려진다.   
>
><span style="color:hotpink">∴적당한 α값을 찾는 것이 중요하다.</span>   



### Reference   
[03 선형회귀_선형 회귀](https://wikidocs.net/53560)
