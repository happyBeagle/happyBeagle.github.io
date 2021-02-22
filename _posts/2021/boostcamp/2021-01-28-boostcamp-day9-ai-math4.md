---
title: "[BoostCamp] DAY9 AI Math#4"
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
- Pandas
toc: true
toc_sticky: true
toc_label: contents
---

# [BoostCamp] DAY9 AI Math#4
---   

## 1. Pandas 활용하기   
이번 수업을 듣다보니 pandas에서 일어나는 연산을 SQL에서도 가능할 것이라 생각을 하였다. 그래서 둘을 비교하며 이해해보기로 하였다.    

### - Group By    
※해당 실습에서는 아래의 데이터를 활용하여 실습한다.  
![image](https://user-images.githubusercontent.com/68745983/106142458-da55dd80-61b4-11eb-9cfc-e5eb4443f487.png)   
#### 1) 그룹으로 묶어보자.
* **pandas** --> df.groupby("Team")["Points"].sum()  
	* Team은 묶음의 기준이 되는 컬럼이다.    
	* Points는 묶음을 적용받는 컬럼이다.   
	* sum()은 적용 받는 연산이다.   
	* ![image](https://user-images.githubusercontent.com/68745983/106140513-38cd8c80-61b2-11eb-9bcc-a604c38b5643.png)   
* **MYSQL** --> SELECT Team, SUM(Points) FROM df GROUP BY Team;   
	* df 테이블에서 Team 컬럼을 기준으로 묶은 뒤 Points 값들을 합하라는 뜻이다.   
	* ![image](https://user-images.githubusercontent.com/68745983/106142524-efcb0780-61b4-11eb-8f95-34bffa5f33b1.png)   

> 여러 그룹으로도 묶을 수 있을 까?    
> * pandas   
> ![image](https://user-images.githubusercontent.com/68745983/106148067-f446ee80-61bb-11eb-84fd-c127af955809.png)   
> * MySQL    
> ![image](https://user-images.githubusercontent.com/68745983/106148307-3f610180-61bc-11eb-9a23-ed86014da2a6.png)   

**At Pandas**   

※ Group by 명령의 결과물도 결국은 dataframe이다.   
※ 두개의 column으로 gruop by를 할 경우, index가 두개 생성된다.   

**PLUS in Padas**   
Pandas에는 Group으로 묶여진 데이터를 matrix 형태로 전환해주는 `ustack`이라는 메소드가 존재한다.   
![image](https://user-images.githubusercontent.com/68745983/106148711-b9918600-61bc-11eb-8910-fe11de193bc9.png)   

> 위의 예제에서는 Team을 기준으로 Year을 나누었다. 그렇다면, Year을 기준으로 나눈 뒤 Team별로 기준을 나눌 수 있을 까?    
> **Pandas**   
> ![image](https://user-images.githubusercontent.com/68745983/106149442-9fa47300-61bd-11eb-98a1-a24b77ff0020.png)   
> 	* swaplevel() 메소드를 통해 기존에 Team, Year순서였던 정렬을 바꿔주었다.    
> 	* sort_index() 메소드를 통해 index를 기준으로 정렬을 한다.    
> 		* 만약, sort_index()에 (현재 year, team 순, default=0) 1의 값을 주었다면 team명을 기준으로 정렬되었을 것이다.   
> **MySQL**   
> ![image](https://user-images.githubusercontent.com/68745983/106150344-9962c680-61be-11eb-8d43-fead24b94605.png)  
> 	* ORDER BY 에는 ASC, DESC의 방법이 존재한다.   
> 		* ASC : 오름차순 정렬    
> 		* DESC : 내림차순 정렬    
> 		* ORDER BY에서 기준이 될 column들은 GROUP BY와 같이 나열하면 된다.  

#### 2) Gruop by로 묶인 df를 추출 가능할까?
**Pandas** --> grouped = df.groupby("Team")   
* ![image](https://user-images.githubusercontent.com/68745983/106151177-6ec53d80-61bf-11eb-9d1f-72dcd87f5f16.png)   
* Team으로 묶인 Group들이 grouped에 할당된 것을 확인할 수 있다.    
	* Tuple 형태로 그룹의 key값과 Value값이 추출된다.   
	* 특정 key값을 가진 그룹의 정보만 추출 가능하다.    
	* ![image](https://user-images.githubusercontent.com/68745983/106151784-0dea3500-61c0-11eb-92f4-18518e04408f.png)   
추출된 group정보에는 세가지 유형의 apply가 가능하다.   
##### Aggregation
요약된 통계정보를 추출해 준다.   
![image](https://user-images.githubusercontent.com/68745983/106153269-b51b9c00-61c1-11eb-93bf-eaf10d1aa2de.png)   
만약 여러 결과(합, 평균 등)을 알고 싶다면 sum, np.mean과 같은 function을 리스트에 넣어서 매개변수로 넘겨주면 된다.   

##### Transformation    
* Key값 별로 요약된 정보가 아니다.    
* 개별 데이터의 변환을 지원한다.    

![image](https://user-images.githubusercontent.com/68745983/106154078-8fdb5d80-61c2-11eb-9a5f-618ee3291ea7.png)

> ※ 알아두자!!   
> max나 min 처럼 Series 데이터에 적용된느 데이터들은 key값을 기준으로 Grouped된 데이터 기준이다.   


##### Filtration   
* 특정 정보를 제거하여 보여주는 필터링 기능이다.   
* 특정 조건으로 데이터를 검색할 때 사용한다.    
![image](https://user-images.githubusercontent.com/68745983/106156532-feb9b600-61c4-11eb-8dc3-51bb6e1d1883.png)   


#### 위에서 배운 내용을 실습해보자.  

![image](https://user-images.githubusercontent.com/68745983/106158204-da5ed900-61c6-11eb-879a-4865b1ea3efe.png)    

우선 우린 위와 같은 데이터를 가지고 실습을 진행할 것이다.   

1. 월별 통화량을 계산해보자.   
![image](https://user-images.githubusercontent.com/68745983/106158716-61ac4c80-61c7-11eb-8ae2-7b4c25e645fd.png)   
월을 기준으로 group을 묶어주고 각 달별 핸드폰 사용량을 합해주면 된다.   

2. 네트워크 종류에 따른 통화량을 알아보려면 어떻게 해야할 까?    
![image](https://user-images.githubusercontent.com/68745983/106160185-e5b30400-61c8-11eb-82d7-6c0919b585c1.png)  
우선 item에서 call값을 가진 row만 추출한다. 그리고 network로 groupby하여 사용량을 합해주면 된다.   

3. 월, 사용 내용에 따른 사용 날짜   
![image](https://user-images.githubusercontent.com/68745983/106160575-52c69980-61c9-11eb-9729-9a5bd268421a.png)   
month오 item으로 grouping을 한다. 그후 그룹화된 데이터 프레임에 date의 갯수를 센다.   
이를 좀더 보이 좋게 `matrix`형태로 나타내보자.   
![image](https://user-images.githubusercontent.com/68745983/106160868-a507ba80-61c9-11eb-9fc8-97538e00a1ef.png)    

4. 여러 데이터를 보여주는 표도 생성 가능할까?   
![image](https://user-images.githubusercontent.com/68745983/106162358-5c510100-61cb-11eb-966d-092e3060eb19.png)   
월간 각 item에 대해 분석해보았다.  
* 사용 기간의 min, max, sum을 보여준다.   
* networktype의 갯수를 세어보았다.
* 사용 날짜들의 min, first, nunique를 구해보았다.

그렇다면 위와 같이 표로도 표현이 가능하다면, 피봇테이블도 만들 수 있지 않을 까?   

### 2. Pivot table & Crosstab   
#### 1) pivot table   
**피봇 테이블(pivot table)이란?** 자신이 원하는 데이터만을 가지고 원하는 행과 열에 데이터를 배치하여 만들어진 새로운 테이블   
그렇다면 판다스에서는 어떻게 pivot테이블을 얻을 수 있을 까?   
![image](https://user-images.githubusercontent.com/68745983/106164405-447a7c80-61cd-11eb-92f4-b9e379cde73d.png)    

* ["duration"]   
	* table을 구성하는 valuesms duration이다.   
* index=[df\_phone.month, df\_phone.item]
	* table의 index를 정해준다.   
	* 해당 예제에서는 month에 따른 item이 index가 된다.   
* columns=df\_phone.network   
	* table을 구성하는 column을 정해준다.   
* aggfunc="sum"  
	* table 값을 어떻게 구성할 것인지 정해준다.
	* default는 평균값이다.   
* fill\_value = 0  
	* 값이 존재하지 않는 cell을 무엇으로 채울지 정한다.  
	* default는 NAN이다.   

#### 2) crosstab   
* 특히 두 칼럼에 교차 빈도, 비율, 덧셈등을 구할때 사용한다.   
* pivot table의 특수한 형태이다.   
* User-Item Rating Matrix 등을 만들 때 사용한다.   
* ** pandas.crosstab(index, columns, values=None, aggfunc=None)**   
	* index : index가 되는 column을 지정해주자.   
	* columns : column이 되는 column을 지정해주자.   
	* value : 해당 index와 columns에따라 분류될 값을 정해준다.   
	* aggfunc : table에 값을 넣을 때 어떤 값을 넣을 것인가?   


### 3. Merge & Concat   
#### 1) merge  
- SQL에서의 Merge와 같은 기능을 가진다.   
- 들어가기전에 join에 대해 알아보자.   
##### Type of join   
![image](https://user-images.githubusercontent.com/68745983/106167456-8fe25a00-61d0-11eb-9aae-99ea3ca4f749.png)    
##### 실습 data   
![image](https://user-images.githubusercontent.com/68745983/106169661-f5cfe100-61d2-11eb-947b-40bd8ac0ae77.png)    

##### left join   
* **At Pandas**    
![image](https://user-images.githubusercontent.com/68745983/106171476-e81b5b00-61d4-11eb-86da-eeca0bc37551.png)   
how에서 어떻게 두 table을 합칠 것인지 정할 수 있다.   
현재는 `left`값을 주었으므로 **Left Join**을 할 것이다.   

* **At SQL**   
![image](https://user-images.githubusercontent.com/68745983/106170927-557abc00-61d4-11eb-97e0-242befd8a4c2.png)   
위의 Pandas에서 실행한 값과 동일하다.   
LEFT 즉, table a의 subject_id를 기준으로 합했기 때문에 table_b에서 같은 subject_id를 가지고 있는 row만 합쳐졌다. 또한, table_b에 존재하지 않아 매칭되지 않은 table_a의 데이터는 NULL로 채워졌다.    

##### RIGHT join   
* **At Pandas**    
![image](https://user-images.githubusercontent.com/68745983/106172107-c2db1c80-61d5-11eb-987a-bb3647fac137.png)

* **At SQL**    
![image](https://user-images.githubusercontent.com/68745983/106172405-249b8680-61d6-11eb-83e3-1d1521623e93.png)

##### FULL(outer) join   

* **At Pandas**    
![image](https://user-images.githubusercontent.com/68745983/106173324-244fbb00-61d7-11eb-83b7-8be30e01fe96.png)

* **At SQL**    
![image](https://user-images.githubusercontent.com/68745983/106173068-dfc41f80-61d6-11eb-8824-73635813a860.png)   
ORACLE에는 FULL JOIN이 존재하지만, MYSQL에는 존재하지 않는다. 즉, RIGHT JOIN과 LEFT JOIN을 UNION해주어야한다.   


##### Inner join   
* **At Pandas**    
![image](https://user-images.githubusercontent.com/68745983/106173763-a17b3000-61d7-11eb-982a-c49bf1e9b0ae.png)   

* **At SQL**    
![image](https://user-images.githubusercontent.com/68745983/106173673-8ad4d900-61d7-11eb-9b83-a150946eba6c.png)   

##### 그 외...
** pd.merge()**    
* on : 합쳐지는 두 테이블 사이에 같은 이름을 가진 column이 있다면 해당 column을 기준으로 join   
	* ex) on="subject_id" 
* left_on, right_on : 왼쪽 오른쪽의 table이 합쳐질 때 key가 되는 column을 지정해준다.   
* left_index, right_index : index를 기준으로 join한다.   

그외에도 다양한 기능들이 있으니 [공식사이트](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.merge.html)에서 알아보자.



## 2.확률론 맛보기

### INTRO. 딥러님에서 확률론이 필요한 이유   
* 딥러닝은 **<span style="color:orange">확률론 기반의 기계학습 이론</span>**에 바탕을 두고 있다.  
* 기계학습에서 사용되는 손실함수들의 작동 원리는 데이터 공간을 통계적으로 해석해서 유도한다.   
	* 회귀 문제 : 손실함수로 이용되는 L2-norm은  **<span style="color:orange">예측 오차의 분산을 가장 최소화하는 방향으로 학습</span>**하도록 유도한다.   
	* 분류문제 : 교차엔트로피는 **<span style="color:orange">모델 예측의 불확실성을 최소화하는 방향으로 학습</span>**하도록 유도한다.   
* 분산, 불확실성을 최소화하기 위해서 -> 측정방법을 알아야한다.   

### 1) 이산 확률 변수 VS 연속 확률 변수   
* 확률 변수는 확률 분포에 따라 **<span style="color:orange">이산형</span>**과 **<span style="color:skyblue">연속형</span>**확률 변수로 구분하게 된다.    
	* <span style="color:orange">이산형</span> : 확률 변수가 가질 수 있는 경우의 수를 모두 고려하여 확률을 더해서 모델링    
	* <span style="color:skyblue">연속형</span> : 데이터 공간에 정의된 확률 변수의 밀도 위 에서의 적분을 통해 모델링   
> 확률분포는 데이터의 초상화이다.   
> * 데이터 공간을 x*y라 표기하고 <i>D</i>는 데이터의 공간에서 데이터를 추출하는 분포이다.    
> 	* <i>D</i>는 이론적으로 존재하는 확률분포이므로 사전에 알수 없다.   
> * 데이터는 확률 변수로 `(X, y) ~ D`라 표기한다.   
> * P(X)는 입력 X에 대한 주변확률 분포로 y에 대한 정보를 주진 않는다.
> * 조건부확률 분포 P(X\|y)는 데이터 공간에서 입력 X와 출력 y 사이의 관계를 리모델링한다.   
> 	* P(X\|y) : 입력 변수 X에 대해 정답이 y일 확률
> 		* 로지스틱 회귀에서 softmax(Wφ + b)은 데이터 x로 부터 추출된 특징패턴 φ과 가중치 행렬 W를 통해 조건부확률 **P(y\|φ)**를 계산한다.   
> 		* 회귀문제에서는 조건부 기대값을 추정한다.

#### 기대값?   
* 확률 분포가 주어지면 데이터를 분석하는데 사용 가능한 여러 종류의 통계적 범함수를 계산할 수 있다.   
* 기대값은 데이터를 대표하는 통계량이다  
* 확률 분포를 통해 다른 통계적 범함수를 계산하는데 사용한다.   
* 기대값을 이용해 분산, 첨도, 공분산등 여러 통계량을 계산할 수 있다.   


### 2) 몬테카를로 샘플링   
* 기계학습의 많은 문제들은 확률분포를 명시적으로 모를 때가 대부분이다.
* 확률 분포를 모를 때 **데이터를 이용하여 기댓값을 계산하려면 <span style="color:orange">몬테카를로 샘플링</span>**을 사용하여야 한다.  
* 몬테카를로 샘플링은 독립추출만 보장된다면 대수의 법칙에 의해 수렴성이 보장된다.   







## 3. 그외 이모저모   
1. 강의  
	- 오늘 Pandas강의는 기존에 알고 있던 SQL과 비슷한 부분이 있어 함께 공부하는 시간을 가져보았다.
	- 확률론 부분은 다소 생소한 내용이 있어 공부하는데 어려움이 있었다. 좀 더 봐야 이해가 잘 될 수 있지 않을까 생각이 된다.
2. 피어 세션  
	- 오늘은 풀스텍 머신러닝 엔지니어링, Pythorch 입문등에 대한 내용을 다룬 세미나를 들었다. 
	- 풀스텍 머신러닝 엔지니어링은 꽤 흥미로운 분야라 앞으로 더 진도가 나간 내용들을 접한다면 정말 재미있을 것같다.   
	- 혼자 공부할때와 다른 시각으로 바라보는 pytorch를 보니 새로웠다. 많은 것들을 배울 수 있을 것같아 기대된다.
3. 나중에라도 공부할 내용
	- https://aldente0630.github.io/data-science/2018/08/05/a-beginners-guide-to-optimizing-pandas-code-for-speed.html  
	- http://www.notespoint.com/pandas-groupby/   
	- https://medium.com/bigdatarepublic/advanced-pandas-optimize-speed-and-memory-a654b53be6c2
