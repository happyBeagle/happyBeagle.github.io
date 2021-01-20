---
title: "[Pytorch]Practice of Linear Regression #2"
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
- LinearRegression
toc: true
toc_sticky: true
toc_label: contents
---

## Practice of Linear Regression #2(feat. PyTorch)   
    
이전 글에서 우리는 집이 지어진 년도에 따른 집가격을 예측해보았다.  
**하지만, 집 가격을 예즉하는 데는 그보다 다양한 요소들이 필요하다.**   
그렇다면 우리는 어떻게 다양한 요소들을 고려하여 결과 값을 예측할 수 있을 까?   

### 다중 선형회귀(Multivariable Linear regression)   
![image](https://user-images.githubusercontent.com/68745983/104887811-42cfde00-59af-11eb-93cf-0bf8eea17b2e.png)   
feature가 여러가지가 존재하는 경우에는 위와 같이 표시할 수 있다.   
이를 좀 더 간단하게 표현한다면, **행렬**을 활용할 수 있다.   
![image](https://user-images.githubusercontent.com/68745983/104890093-68aab200-59b2-11eb-8a1f-f0851298814e.png)   
위와 같이 하나의 데이터 뿐만아니라 여러 데이터를 엮어서 계산가능하다.  
그렇다면, 집가격 예측을 통해 실습을 해보자.   

#### 1.데이터를 가져오자.   
##### 1)데이터의 내용을 확인해보자.   
![image](https://user-images.githubusercontent.com/68745983/104899513-49b21d00-59be-11eb-923f-41eb45f01fe3.png)  
학습 데이터를 살펴보면 숫자 데이터가 아닌 것, 데이터에 NAN이 포함된 것 등 다양한 형태의 데이터가 존재하는 것을 알 수 있다.   
우리는 숫자데이터만을 가지고 학습을 할 것이다.  
그렇다면 숫자데이터만을 어떻게 필터링해서 가져 올 수 있을 까?   
###### - 1. 숫자데이터만을 가져오자.   
![image](https://user-images.githubusercontent.com/68745983/104903896-eaefa200-59c3-11eb-94ae-faf357037528.png)   
* **data.select_dtypes(include=[])**   
	해당 메소드를 통해 남길 자료형과 제외시킬 자료형을 정할 수 있다.   
    *Return a subset of the DataFrame’s columns based on the column dtypes.*  
    - include   
    	return될 subset에 포함되는 자료형을 정해 준다.   
    - exclude   
    	return될 subset에 포함되지 않는 자료형을 정해준다.   
###### - 2. NAN데이터를 처리해보자.   
![image](https://user-images.githubusercontent.com/68745983/104906543-2fc90800-59c7-11eb-81ba-3e9df33eeaa1.png)   
* **data.isnull()** 
	isnull메소드를 사용하면 각각의 요소들이 null인지 아닌지를 판단해준다.   
    하지만 아주 많은 데이터를 하나하나 확인하기에는 비효율적이다.   
    이를 해결하기 위해 우리는 뒤에 any()메소드를 추가하여 실행한다.   
    any()메소드와 함께 실행을 할 경우, 위와 같이    
    <span style="color:red">**null이 나타나는 column에는 True로 나타난다.**</span>   

그렇다면 우리는 null을 어떻게 처리해야할까?   
1. 모두 0로 만들어 학습시킨다.   
2. NAN이 들어간 column이나 row를 삭제하여 학습시킨다.   

1번의 경우에는 학습을 할때, 정확도를 낮출 가능성이있다.  
그래서 나는 해당 column을 삭제하여 학습시키도록 하겠다.   
(※만약  label이 되는 SalePrice가 true였다면, 우선 NAN이되는 row를 삭제하고 살펴 봐야할 듯하다.)   
![image](https://user-images.githubusercontent.com/68745983/104908716-3016d280-59ca-11eb-8160-dea6862455f2.png)   
* **data.dropna()**   
	NAN 값을 삭제한다.   
    - axis
    	- 0 or index : 특정 row에 NAN값이 존재한다면, 해당 row를 drop한다. 
    	- 1 or columns : 특정 column에 NAN값이 존재한다면, 해당 column을 drop한다.   
    - how   
    	- any : 특정 row나 column(axis에 의해 정해진 기준)에 NAN이 하나라도 있으면 drop한다.
    	- all : 특정 row나 column(axis에 의해 정해진 기준)가 모두 NAN이면 drop한다.   

##### 2)train data와 test data를 구분하자.   
![image](https://user-images.githubusercontent.com/68745983/104923343-454a2c00-59df-11eb-9f93-0cf33ad68a45.png)   
#### 2.학습을 시키자.   
##### 1)bath, epoch등 학습을 시킬 횟수 등을 정해준다.   
![image](https://user-images.githubusercontent.com/68745983/104912697-f21cad00-59cf-11eb-9392-4e7aa8d36448.png)   
##### 2)학습을 해보자.   
![image](https://user-images.githubusercontent.com/68745983/104923930-1aaca300-59e0-11eb-8f43-6236c315968e.png)   
위의 코드는 행렬의 곱셈부분을 제외하고는 앞선 글의 코드와 동일하다.   
자, 그럼 결과를 확인해보자.   
![image](https://user-images.githubusercontent.com/68745983/104928183-b096fc80-59e5-11eb-9b5a-eb15f80a9a8e.png)   
**<span style="color:red">????????????????????????????????????????</span>**   
**<span style="color:red">????????????????????????????????????????</span>**   
이게 뭘까? 왜이럴까???? learning rate도 적당한거나 좀 작은 것 같은데 왜 이럴까...???
**데이터 Normalization을 해보자!!!**   
###### Normalization?   
> 정규화란 무엇일까??   
> unnormalization된 data에 대해서 알아보자.   
> ![image](https://user-images.githubusercontent.com/68745983/104930109-108ea280-59e8-11eb-9df6-8cdca9e1de17.png)   
> 위의 그래프가 unormalization된 데이터이다 이를 가지고   
> **경사하강법**을 이용해 최적화를 진행한다고 생각해보자.   
> 각 위치마다 range가 달라서 자칫하다 **over shooting**이 발생할 가능성이 있다.  
> 그래서 우리는 데이터를 **Normalization**시켜주는 것이다.  
> > 그러면 어떻게 Normalization을 시켜줄 수 있을까?   
> > ![image](https://user-images.githubusercontent.com/68745983/104932009-88f66300-59ea-11eb-8d48-8276ac52ac7a.png)   
> > 위의 공식은 minMax Normalization에 대한 공식이다.   
> > 각각의 요소들을 해당 요소가 속하는 feature에서 가장 큰 값과 작은 값을 사용하여 연산을 해준다.   
> > 그렇게 되면 데이터들이 정규화 되어 아래와 같이 변할 것이다.   
> > ![image](https://user-images.githubusercontent.com/68745983/104932780-66187e80-59eb-11eb-8abc-c9cc455f50fc.png)   
> 
> **<span style="color:red">그런데 또 standardization은 또 뭘까?</span>**  
> standardization(표준화)또한 데이터를 조금 더 고르게 만들기 위해 사용되는 방법이다.   
> >그렇다면 어떻게 standardization을 할 수 있을까?   
> >![image](https://user-images.githubusercontent.com/68745983/105057013-2370a800-5ab8-11eb-8dcd-354e309cfa51.png)   
> >위의 공식을 통해 데이터를 좀더 다듬어서 local minima에 빠지는 것을 방지한다.   
>
> **그렇다면, 두가지 기법의 차이점과 공통점은 무엇일까?**   
> ![image](https://user-images.githubusercontent.com/68745983/105062857-6afa3280-5abe-11eb-9902-90a90839f843.png)



우리가 가진 데이터를 확인하면 아래와 같이 각각의 feature가 가진 값들의 차가 크다는 것을 알 수 있다.   
![image](https://user-images.githubusercontent.com/68745983/104908716-3016d280-59ca-11eb-8160-dea6862455f2.png)   
그래서 값들은 0~1사이의 값으로 평준화해주는 normalization을 선택하여 데이터를 scaling해주었다.   
![image](https://user-images.githubusercontent.com/68745983/105195181-b7f10e00-5b7d-11eb-849b-7c9569a574f7.png)   

##### 3) 다시 학습을 해보자.   

![image](https://user-images.githubusercontent.com/68745983/105195747-45ccf900-5b7e-11eb-9aaa-9b7ca23d4768.png)   
다시 학습을 하며 epoch값을 500으로 증가 시켜주었다. 또한 learning_rate를 1e-4로 증가 시켜주었다.  
![image](https://user-images.githubusercontent.com/68745983/105195917-71e87a00-5b7e-11eb-87b7-b3f21e730064.png)   
학습을 시켜보니 위와 같이 cost값이 감소하였다.  
이것을 좀 더 보기 좋게 그래프로 표현해보자.   
![image](https://user-images.githubusercontent.com/68745983/105196298-d3104d80-5b7e-11eb-955f-8572d48ce10b.png)   
하지만 마지막 cost값을 보면 아직까지 cost값이 크다는 것을 느낄 수 있다.   
같은 epoch내에서 어떻게 더 정확한 값을 에측할 수 있을까?   
우리는 이전에 숫자로 된 데이터만 가지고 와서 학습을 시켰다.   

그렇다면 이제는 NAN이 있는 데이터를 제외한 모든 feature를 가지고 학습을 하는 방법에 대해 차차 알아보자.(언젠간 ㅎㅎㅎ)   

###  Reference   
[03 선형회귀_다중 선형회귀](https://wikidocs.net/54841)   
[data set_house prices](https://www.kaggle.com/c/house-prices-advanced-regression-techniques)   
[pandas dropna](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.dropna.html)   
[pandas select_dtypes](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.select_dtypes.html)  
[Normalization VS Standardization](https://www.analyticsvidhya.com/blog/2020/04/feature-scaling-machine-learning-normalization-standardization/)
