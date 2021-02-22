---
title: "[BoostCamp] DAY7 AI Math#2"
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
toc: true
toc_sticky: true
toc_label: contents
---

# [BoostCamp] DAY7 AI Math#2
---   

## 1. What is Gradient Descent?    
### 1) 들어가기전에....    
#### -미분이란??   
* 미분은 **<span style="color:orange">변수의 움직임에 따른 함수값의 변화를 측정하기 위한 도구</span>**이며, 최적화에서 가장 많이 사용하는 기법이다.    
![image](https://user-images.githubusercontent.com/68745983/105794800-1a5b6b80-5fcf-11eb-9388-b0ee125ff6ff.png)    
* 최근에는 미분을 컴퓨터로도 계산 가능하다.   
![image](https://user-images.githubusercontent.com/68745983/105821565-5954e580-5ffe-11eb-95b6-fa9d906186bd.png)    
* 미분 f\`(x)는 함수 f(x)에서 점(x, f(x))에서의 **<span style="color:orange">접선의 기울기</span>**를 나타낸다.   
* 한 점에서 접선의 기울기를 알면 어느 방향으로 움직여야 함수 값이 **<span style="color:red">증가</span>**하는 지 **<span style="color:blue">감소</span>**하는지 알 수 있다.    
	* **<span style="color:red">증가</span>** 시키고 싶다면 미분값을 **<span style="color:red">더한다.</span>**    
	* **<span style="color:blue">감소</span>** 시키고 싶다면 미분값을 **<span style="color:blue">뺀다.</span>**    

* 위의 특성을 이용하여 **<span style="color:red">경사 상승법</span>**을 통해 **<span style="color:red">극댓값의 위치</span>**를 구할 수 있다.   
* 위의 특성을 이용하여 **<span style="color:blue">경사 하강법</span>**을 통해 **<span style="color:blue">극솟값의 위치</span>**을 구할 수 있다.  

> ※ 경사 상승법의 활용  
> 경사 상승법은 극댓값을 구하는 방법들 중 하나이다.  
> 즉, 하나의 특성이있을 때 그 특성을 조금 더 돋보이게 표현을 할 수 있다.    
> 이러한 점을 이용하여 학습을 하기 전 데이터의 전처리 과정에서 원하는 특성을 더 잘 찾게 하기위해 사용될 수 있다.   

> ※ 경사 하강법을 알고리즘으로 이해해 보자.   
> ```
> func(gradient, init, lr, eps) :   
> #gradient : 미분을 계산하는 함수   
> #init : 시작 지점   
> #lr:학습률   
> #esp:학습 종료 조건   
>   
>  var = init   
>  grad = gradient(var) //var값의 위치에서의 기울기   
>  while(abs(grad) > eps):   
> 		var = var - lr * grad   
>  		grad = gradient(var)    
> ```
> 파이썬으로는 아래와 같이 구현 가능하다.   
> ![image](https://user-images.githubusercontent.com/68745983/105826979-bfdd0200-6004-11eb-8ebf-67e2b5e249c3.png)   

##### 변수가 벡터일때는 어떻게 미분하나요?   
* 벡터가 입력인 다변수 함수의 경우 **<span style="color:orange">편미분</span>**을 사용한다.   
* 각 변수 별로 편미분을 계산한 **<span style="color:orange">그레디언트 벡터</span>**를 이용하여 경사하강 or 상승방법을 사용할 수 있다.   
* 벡터에서는 경사하강법을 연산할 때 **<span style="color:orange">abs 연산</span>** 대신, **<span style="color:orange">Norm</span>**을 사용하여 연산한다.   
### 2) 경사하강법으로 선형회귀 계수를 구하자.  
선형 회귀의 목적은 `||y - Xβ||2`을 최소화 하는 β를 찾아야한다. 즉 아래와 같은 그레디언트 벡터를 구해야만 한다.   
![image](https://user-images.githubusercontent.com/68745983/105828348-5fe75b00-6006-11eb-9625-3d2cdf88f389.png)   
이들 중 하나를 선택하여 연산해보자.   
![image](https://user-images.githubusercontent.com/68745983/105829100-4692de80-6007-11eb-8bbe-b9674ab1dc85.png)   
이제 우리는 위의 식을 통해 경사하강법을 이용하여 식을 최소화하는 β를 찾을 수 있다.   
![image](https://user-images.githubusercontent.com/68745983/105829885-3af3e780-6008-11eb-96cf-961617687855.png)   

> ※ 경사 하강법 기반 선형회귀 알고리즘으로 이해해 보자.   
> ```
> func(X, y, lr, T) :   
>  #lr:학습률   
>  #T:학습 종료 조건   
>     
>  for t in range(T): // **TIP**  
>  		cost = y - X @ beta
>  		grad = -transpose(X) @ cost   
>  		beta = beta - lr * grad   
> ```
> [TIP]   
> 기존에 경사 하강법에서는 목표 기울기를 준다음 목표기울기에 해당하는 값을 찾을 수 있을 때까지 계속해서 연산을 하였다.   
> 하지만, 이번에는 일정 학습횟수를 부여하여 문제를 풀었다.  
> 두가지 방법 중 어떤 방법이 더 좋다고는 단정하지 못하겠다.   
> 다만, 학습을 진행할 때, 시간, 자원, 효율성등을 고려하면다면 일정 학습횟수를 부여하여 문제를 푸는 것이 좋을 듯하다.    
> 파이썬으로는 아래와 같이 구현 가능하다.   
> ![image](https://user-images.githubusercontent.com/68745983/105836620-c96c6700-6010-11eb-8684-280f5faf3bc5.png)   


### 3) 경사하강법이 만능이라구?    
* 이론적으로 경사하강법은 미분가능하고 볼록한 함수에 대해선 **<span style="color:orange">적절한 학습률과 학습횟수를 선택했을 때 수렴이 보장</span>**되어 있다.   
* 특히 선형회귀의 경우 `||y - Xβ||2`에서 회귀계수 β에 대해 볼록함수이기 때문에 수렴이 보장된다.  
* But 비선셩회위 문제의 경우 식이 볼록하지 않을 수 있으므로 수렴이 항상 보장되지 않는다.   
	* ex) 극솟값, 극댓값이 두개 이상인 경우   


> ※ Tip 확률적 경사하강법이란?    
> * 모든 데이터를 사용해서 업데이트를 하는 대신에 **<span style="color:orange">데이터를 한개 또는 일부 활용하여 업데이트</span>**한다.   
> * 볼록이 아닌 경우 SGD를 통해 최적화 가능하다.   
> 	* SGD라고 해서 만능은 아니다. 다만, <span style="color:green">SDG가 경사하강법보다 실증적으로 더 낫다</span>고 검증되었다.   
> * SGD는 데이터의 일부~~미니 배치~~를 가지고 패러미터를 업데이트하기 때문에 연산자원을 좀 더 활용하는데 도움이 된다. 



## 2. 그외 이모저모   
1. 강의  
	- 혼자서 공부하면서 SGD를 알아봐야지 생각을 하고 있다가 하고 있지 못했었다. 이번기회를 통해 알아 볼 수 있어서 좋았다.   
2. 피어 세션  
	- 내일부터 각자 공부해온 것들을 세미나를 하기로 하였다. 기대된다.
