---
title: "[BoostCamp] DAY8 AI Math#3"
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

# [BoostCamp] DAY8 AI Math#3
---   

## 1. Let study about Pandas   

판다스랑 구조화된 데잍터의 처리를 지원하는 Python 라이브러이이다. ~~Python계의 엑셀~~   
 * 고성능 array계산 라이브러리인 **Numpy**를 통합하여 강력한 스프레드 시트를 제공한다.   
 * 인덱싱, 연산, 전처리 등이 가능하다.   
 * 주로 데이터 처리 및 통계 분석을 위해 사용된다.   
![image](https://user-images.githubusercontent.com/68745983/105985503-e1aab780-60de-11eb-80df-0fb47c387cbd.png)   

### Pandas를 사용해보자.   
#### 1) series   
DataFrame 중 하나의 Column에 해당하는 데이터의 모음이다.    
![image](https://user-images.githubusercontent.com/68745983/105986939-e8d2c500-60e0-11eb-8410-05a7f99efc48.png)   
위와 같이 column vector를 Series로 나타낼 수 있다.   
더불어 아래와 같이 표현해준다면 Index가 기본의 0으로 시작하는 숫자가 아니라 지정된 배열로 나타낼 수 있다.    

```python   
list_data = [1, 2, 3, 4, 5]
list_name = ['a', 'b', 'c', 'd', 'e']

example_obj = Series(data=list_data, index=list_name)   
```   

> **Series의 값은 수정가능할까?**   
> ```python    
> example_obj["a"] = 3.2
> # "a"라는 인덱스르 가진 data에 접근하여 3.2로 값을 수정한다.
> #    
> example_obj.values  # 값리스트만 가져온다.   
> example_obj.index   # 인덱스 리스트만 가져온다.
> ```   


#### 2) dataframe   
Data Table 전체를 포함하는 object  
* 각각의 column은 다른 type을 가질 수 있다.   
* Series를 모아서 만든 Data Table이다 = 기본 2차원이다.    
* `pd.DataFrame(data, index, columns, dtype)`을 통해 dataframe객체를 생성할 수 있다.   
* 하지만, 주로 read_csv 메소드를 통해 파일에서 데이터를 읽어와 dataframe을 생성한다.   

```python   
DataFrame(data, colums=['name', 'age'])   

#column 추가
df = DataFrame(data, columns=['nick_name', 'city', 'name', 'age'])   

#column 선택해서 series 추출하기   
df.name

df["name"]   

```

> loc VS iloc   
> * loc : index location  
> 즉, loc는 index이름을 기반으로 탐색한다.   
> * iloc : index number   
> 즉, iloc는 index번호를 기반으로 탐색한다.  

```python   
df.test = df.age > 20   

#transpose
df.T   

#value만 출력   
df.values  

#csv 변환   
df.to_csv()
```   

#### 3) selection & drop   

* **selection**   

```python      
#한 개의 column선택
df["name"].head()  

#여러개의 column 선택
df[["name", "age", ..]].haed()

#column 이름 없이 사용하는 index number는 row 기준
df[:3]

#column 이름과 함께 row index사용 시, 해당 column만   
df["name"][:3]  

#조건에 따른 data탐색  
df[age < 20]

#select   
df[["name", "age"]][:2]
df.loc[[0, 1], ["name", "age"]]  
df.iloc[:2, :2]   


```    

* **data drop**   

```python   
#index number로 drop
df.drop(1)   #리스트로 넘겨준다면 여러개를 한꺼번에 삭제 가능하다.   

#axis지정으로 축을 기준으로 drop   
df.drop("name", axis=1) # axis = 0 row, axis = 1 column   

del df["name"]

```    

#### 4) dataframe operations   
* **series operation**   
	* index 기준으로 연산을 수행하며, 겹치는 index가 없을 경우 NaN으로 반환한다.   
* **dataframe operation**   
	* df는 column과 index를 모두 고려한다. ex) add operation을 쓰면 NaN값으로 0을 반환한다. 이외에도 sub, div, mul이 있다.   
* **series + dataframe operation**   
	* axis를 기준으로 row broadcasting을 수행한다.   

#### 5) lambda, map, apply   
* **map for series**   
	* pandas의 series type의 데이터에도 map 함수를 사용가능하다.    
  
	```python    
	
	 s1 = pd.Series(np.arange(10))
	 s1.map(lambda x : x \*\*2)   
     
    #dict type으로 데이터 교체, 없는 경우 NaN
	 d = {1 : 'a', 2 : 'b', 3 : 'c'}   
     
     s1.map(d)     
     
		 #같은 위치의 데이터를 s2로 전환   
     S2 = Series(np.arrange(10, 20))
     
     #중복되지않는 요소 추출
     df.age.unique()
     df['age'] = df.age.map({12 :"열두 살", 20 :"스무살"})
     
	```    
    
* **replace function**   
	* Map 함수의 기능 중 데이터 변환 기능만 담당한다.  
	* 데이터 변환시 많이 사용하는 함수이다.   

```python   
	df.age.replce({12 :"열두 살", 20 :"스무 살"})
```   


* **apply for dataframe**   
	* 내장 연산 함수를 사용할 때도 똑같은 효과를 얻을 수 있음
	* mean, std등 사용이 가능하다.
	* map과 달리 series 전체에 해당 함수를 적용할 수 있다.  
	* 입력값을 series 데이터로 입력 받아 handling 가능하다.   
	* scalar 값 이외에 series값의 반환도 가능하다.


> ※ applymap    
> * series 단위가 아니니 element단위로 함수를 적용한다.    
> * series 단위에 apply를 적용시킬 때와 같은 효과를 가진다.    

#### 5) pandas 내장함수   
 * **describe()**   
 	* Numeric type 데이터의 요약 정보를 보여준다.  
 * **unique()**   
 	* series data의 유일한 값을 list로 반환한다.   
 * **sum()**   
 	* 기본적인 column 또는 row 값의 연산을 지원   
 	* sub, mean, min, max, count, median, mad, var 등   
 * **isnull()**   
 	* column 또는 row 값의 NaN (null) 값의 index를 반환함   
 * **sort_values**  
 	* column 값을 기준으로 데이터를 sorting   

## 2. 딥러닝 학습방법 이해하기   

### Softmax 연산  
* softmax 함수는 모델의 **<span style="color:orange">모델의 출력을 확률로 해석</span>**할 수 있게 변환해주는 연산이다.  
* 분류 문제를 풀때 선형모델과 소프트맥스 함수를 결합하여 예측한다.   
![image](https://user-images.githubusercontent.com/68745983/105996895-48839d00-60ee-11eb-8be4-34fe6077e9b0.png)   

### 신경망  
* 신경망은 선형모델 + 활성함수 이다.   

#### 1) 활성함수란?    
* 활성함수는 실수 위에 정의된 비선형함수로서 딥러닝에서 중요한 개념이다.    
* 활성함수를 쓰지 않으면 딥러닝은 선형모형과 차이가 없다.   
* 전통적으로 sigmoidsk tanh함수를 많이 사용하였지만, 딥러닝에서는 ReLU함수를 많이 사용한다.   
* 다층 퍼셉트론은 신경망이 여러층이 합성된 함수이다.   

> 층을 여러개 쌓는 이유?   
> - 이론적으로는 2층 신경망으로도 임의의 연속함수를 근사할 수 있다.   
> - 그러나 층이 깊을 수록 목적함수를 근사하는데 필요한 노드의 숫자가 훨씬 빨리 줄어들어 좀더 효율적으로 학습이 가능하다.    


### 딥러닝의 학습 원리 : backpropagation   
* 딥러닝은 **<span style="color:orange">backpropagation 알고리즘</span>**을 이용하여 각 층에 사용된 패러미터를 학습한다.   
* 각 층 패러미터의 그레디언트 벡터는 윗층으로부터 역순으로 계산한다.  



## 3. 그외 이모저모   
1. 강의  
	- 뭔가 들어오던 다른 강의와 진도가 다르게 나가서 당황했다. 어찌보면 같은 순서였겠으나 logistic에 관한 설명 없이 바로 softmax로 건너뛰는 것이 신기했다.   
2. 피어 세션  
	- 오늘부터 각자 공부해오며 세미나를 가졌다. 우리 팀은 추천 시스템 기초에 대해 공부하고 발표하였는 데, 더 배울 것이 많아지는 것이 좋았다.
