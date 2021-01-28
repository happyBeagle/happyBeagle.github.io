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



 
 

더 추가할 내용 有
## 2.확률론 맛보기

//TODO내용 채울것








## 3. 그외 이모저모   
1. 강의  
	- 오늘 Pandas강의는 
2. 피어 세션  
	- 오늘부터 각자 공부해오며 세미나를 가졌다. 우리 팀은 추천 시스템 기초에 대해 공부하고 발표하였는 데, 더 배울 것이 많아지는 것이 좋았다.
