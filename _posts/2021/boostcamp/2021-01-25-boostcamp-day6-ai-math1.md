---
title: "[BoostCamp] DAY6 AI Math#1"
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
- BoostCamp_AI_Tech
tags:
- BoostCamp_AI_Tech
---

# [BoostCamp] DAY6 AI Math#1
---   

## 1. What is Vector?    
우리가 고등학생 때 배운 수학에선 **스칼라는 양, 벡터는 양 + 방향**이런 식으로 구분을 해서 배웠다. 그렇다면 AI에서는 vector를 어떻게 바라보고, 활용할 지 알아보자.   

* 벡터는 숫자를 원소로 가지는 **<span style="color:orange">list</span>** 또는 **<span style="color:orange">array</span>**이다.      
* 벡터는 공간에서 **<span style="color:orange">한 점</span>**을 나타낸다.   
* 벡터는 원점으로부터 상대적 위치를 나타낸다.   
* 벡터는 **\*스칼라 곱**을 통해 길이 변환이 가능하다
* 같은 모양의 두개의 백터가 있다면 성분 합, 성분 곱이 가능하다.  

> 스칼라곱??
> 벡터의 각요소에 같은 수 a가 곱해졌다고 하면, a와 벡터를 스칼라곱했다고 한다.   

### 1) Norm?
Norm(노름)은 **<span style="color:orange">원점에서부터의 거리</span>**를 나타낸다.   

#### - L1-Norm
각 성분의 변화량의 절대값의 합  
![image](https://user-images.githubusercontent.com/68745983/105697630-20f2d000-5f48-11eb-8fb4-1042d2d1125e.png)   

```python  
def l1_norm(x):
	val = np.abs(x)
    val = np.sum(val)
    
	return val
```   

#### - L2-Norm   
파타고라스의 정리를 이용해 유클리드 거리 계산  
![image](https://user-images.githubusercontent.com/68745983/105698066-b9895000-5f48-11eb-850b-0194f80ee3dc.png)

```python   
def l2_norm(x):
	val = x * x
    val = np.sum(val)
    val = np.sqrt(val)
    
    return val
```   

#### 두가지의 norm 측정법은 머신러닝에서 어떻게 활용될까?   
* 각각의 norm측정법의 연산과정을 살펴보면 **outlier**가 심할 수록 제곱으로 그 합을 구하는 L2의 경우 더 큰 수치로 적용이 되기 때문에 **outlier**가 적당히 무시되기를 원한다면, L1으로 loss값을 계산하는 것이 더 좋을 수 있다.   
* **outlier**가 심하지 않은 데이터를 기준으로 보았을 때, L2계산법이 L1보다 데이터의 변화에 더 민감하다는 것을 볼 수 있다.    

### 2) 벡터의 연산    
#### - 두 벡터 사이의 거리   
![image](https://user-images.githubusercontent.com/68745983/105700632-7b8e2b00-5f4c-11eb-9456-c98bc1300f7f.png)   
두 벡터 사이의 거리는 어떻게 구하면 될까?   
L1, L2-norm을 통해 계산이 가능하다.  
두 벡터의 뺄셈을 이용하면 된다. 거꾸로 연산하여도 거리는 동일하다.   

#### - 두 벡터 사이의 각도   
![image](https://user-images.githubusercontent.com/68745983/105701029-0cfd9d00-5f4d-11eb-8886-a77e23bd9f5b.png)   
제 2 코사인 법칙을 활용하면 된다.    
![image](https://user-images.githubusercontent.com/68745983/105701766-28b57300-5f4e-11eb-8a1f-d60690df7140.png)  
이를 역함수(arccos)를 이용하여 각도를 구할 수 있다.   


## 2. What is Matrix?    
* 벡터를 원소로 가지는 **<span style="color:orange">2차원 배열</span>**이다.   
* 행렬 => 행(row) * 열(column)으로 이루어져있다.   
* 특정 행이나 열을 고정하면 열(행)벡터라고 한다.   
* 벡터가 공간에서 한 점을 의미한다면 행렬은 **<span style="color:orange">여러 점들</span>**을 나타낸다.  
* 행렬끼리 같은 모양을 가졌을 때, 덧셈, 뺄셈을 할 수 있다.   
* 성분곱, 스칼라곱은 벡터와 동일하다.   

### 1) 행렬 곱셈   
![image](https://user-images.githubusercontent.com/68745983/105703369-77fca300-5f50-11eb-9435-ed5c256aad18.png)   
행렬 곱셈은 위와 같이 수식으로 나타낼 수 있다.   

```python  
#numpy에서 행렬곱셈  
x @ y
```    

> ※ 행렬에도 내적이 있을까?   
> np.inner으로 내적이 가능하다.
> i번째 행벡터와 j번째 행벡터 사이의 낵적을 성분으로 가지는 행렬을 구한다.

* 행렬곱을 통해 벡터를 다른 차원의 공간으로 보낼 수 있다.
* 행렬곱을 통해 패턴을 추출할 수 있고 데이터를 압축할 수 도 있다.   


### 2) 역행렬   
어떤 행렬 A의 연산을 거꾸로 되돌리는 행렬을 **<span style="color:orange">역행렬</span>**이라 부르고 A^(-1)라 표기한다.  

※ 역행렬은 행과 열 숫자가 같고 행렬식이 0이 아닌 경우에만 계산할 수 있다.   

```python   
np.linalg.inv(x)
```   

> 그렇다면 행과 열 숫자가 다르거나, 행렬식이 0인 경우에는 역행렬을 구할 수 없을까?    
> **유사 역행렬 또는 무어-펜로즈 역행렬**에 대해 알아보자.   
> ![image](https://user-images.githubusercontent.com/68745983/105705160-26094c80-5f53-11eb-9528-80ab4178b7e3.png)  
> 그렇다면 numpy에서는 이를 어떻게 구할 수 있을 까?    
> ```python   
> np.linalg.pinv(x)
 ```   
 
 
 * 우리는 행렬을 이용해 연립방정식의 해를 구할 수 있다. 
 * 우리는 행렬을 이용해 선형회귀식을 찾을 수 있다. --> 데이터  및 feature가 많을 수록 시간이 많이 듬 : 효율성이 떨어짐


 



## 3. 그외 이모저모   
1. 강의  
	- 수학 공부는 대학생때 했던 것 외에는 별도로 있지 않아 중간 중간 알려주시는 팁들을 생각하며 공부하고 있다.  
	- 앞으로의 학습이 기대된다.   
2. 피어 세션  
	- 현재 프로젝트를 위한 기본지식에 대해 공부하기로 하였다.
	- 추천 시스템은 처음 공부하는데 기대된다.  

## 4. Reference   
[L1 norm VS L2 norm](https://www.stand-firm-peter.me/2018/09/24/l1l2/)
