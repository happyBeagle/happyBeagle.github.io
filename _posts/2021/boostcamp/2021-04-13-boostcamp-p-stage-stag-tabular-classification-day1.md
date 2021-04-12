---
title: "[BoostCamp] P-stage stag Tabular Classification day1"
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
toc: true
toc_sticky: true
toc_label: true
categories:
- BoostCamp_AI_Tech
tags:
- Pstage_Tabluar_Classification
---

# [BoostCamp] P-stage stage2 정형 데이터 분류 day1  
---   

## 오늘의 목표

1. EDA를 해보자.

## 1. EDA

### 주어진 항목들에 대해 이해해보자.

1. `data.info()`   
우선 데이터들엔 어떤 column들이 존재하는 지 파악해야했다. 그래서 `pandas`의 `describ()`메소드를 활용하여 column들의 정보를 파악해보았다.   

![image](https://user-images.githubusercontent.com/68745983/114416645-d8b08900-9beb-11eb-8187-862a63d1c2e9.png)

그러면 각각의 column들의 내용을 파악하여 어떻게 분석을 할지 고민해보자.    

	* order_id : 주문 id이다. 아마 각 주문들을 구분하기 위해 사용되어지는 것같다.    
	* product_id : 주문한 제품의 식별자이다.   
	* description : 각 제품을 설명하는 요소이다.   
	* quantity : 주문 수량을 의미하는 요소이다.    
	* price : 제품의 가격이다.   
	* customer_id : 고객의 식별자이다.    
	* country : 고객의 국적을 의미한다.   
	* total : 총 주문 금액이다.   

어떻게 분류를 해야 잘했다고 소문이 날지 고민을 하였다.    
그런데 우리가 예측해야하는 것은 2011년 12월의 고객의 총 구매금액이 300을 넘길 확률이다.    
그렇다면 **12월**이라는 키워드에 집중해서 고민해보면 어떨까?    

### 12월\.\.\.\.?    

현재 많이 보편화된 기념일이지만, 생각해보면 12월 25일은 크리스마스로서 크리스찬들에게 큰 의미를 가지는 날이다.   
그렇다면 크리스찬이 많은 서구쪽이 많은 지 확인을 해보는 것도 좋을 것같다.   
더불어 12월은 겨울이다. 그래서 북반구의 경우 겨울용품을 사는 경향이 있을 것이고 남반구가 많다면 여름 용품의 구매가 우세할 것으로 예측된다.   

### 나라별로 한번 구분해보자.    

![image](https://user-images.githubusercontent.com/68745983/114418370-6771d580-9bed-11eb-9e70-007929933f0e.png)   

* 영국이 너무 수적으로 많아 영국만을 고려해도 무방한 비율이 나왔다.    
* 물론, 대륙별로 정리해도 유럽이 우세하겠지만 나머지 나라들이 다른 대륙에 몰려있는 것도 생각해볼 수 있으니, 대륙별로도 구분해보았다.    

![image](https://user-images.githubusercontent.com/68745983/114418679-b881c980-9bed-11eb-99fa-4ec2cc15f1e4.png)   

* 사실, 유럽외에는 모르겠닼ㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋ
* 그럼 이제 12월에는 어떤 상품들이 주로 팔리는지 확인해보자.    

### 월별 구매 상품 카테고리    

![image](https://user-images.githubusercontent.com/68745983/114418902-eb2bc200-9bed-11eb-85e9-a6274d1ad4cb.png)   

* 21, 22, 23번의 카테고리에 속하는 상품들을 주로 많이 구매한다는 것을 확인할 수 있다.    
* 그래도 각각의 요소들의 가격을 고려하여 계산하면 다른 결과값을 얻을 수 있으니 해당 부분도 고려해 보자.   

![image](https://user-images.githubusercontent.com/68745983/114419299-452c8780-9bee-11eb-9df0-89fdc78fa7cd.png)    

* 위의 구매량만 고려한 그래프보다 밝은 부분 즉, 높은 가격에 해당하는 부분이 더 늘어 난것을 확인할 수 있다.   
* 그렇다면 해당 카테고리에 속하는 상품들에는 어떤 것이 있을까?    


### word cload 구해보기    

1. 20번 카테고리의 상품   
	* ![image](https://user-images.githubusercontent.com/68745983/114429209-10253280-9bf8-11eb-9020-4cbcb2d5bc88.png)    
	* 점심, 가방 등이 눈에 띄이며 특히, 가방, 박스와 관련한 단어들이 자주 보인다.   
	* 가방과 같은 잡화를 포함하는 분류로 여겨진다.   
2. 21번 카테고리의 상품   
	* ![image](https://user-images.githubusercontent.com/68745983/114430244-326b8000-9bf9-11eb-94b6-6a1c2a09afc9.png)   
	* 물병과 같은 잡화 부분을 분류하는 카테고리인듯한다.

3. 22번 카테고리의 상품    
	* ![image](https://user-images.githubusercontent.com/68745983/114429551-77db7d80-9bf8-11eb-8247-246780d4a5d7.png)   
	* 20번 제품과 크게 차이는 보이지 않는다.   
	* 간혹 lunch, water과 같은 식품에 관련한 단어는 보이지만 design, chain, clock등이 자주 보이는 것으로 봐서 잡화에 가까운 상품들을 주로 포함할 것으로 사료된다.    
4. 23번 카테고리의 상품    
	* ![image](https://user-images.githubusercontent.com/68745983/114430011-ecaeb780-9bf8-11eb-82df-50eed570f7ae.png)    
	* 빈티지, 가방 등의 상품들이 존재하는 것같다.   

* 현재까지 그 상품들을 확인해보기에는 크리스마스에 관련된 상품보다 블랙프라이데이에 맞춰진 상품들이 11~12월쯤에 많이 팔렸고   
* 더불어 해당 상품들이 평소에도 매출의 큰 부분을 차지한다고 볼 수 있을것같다.   
* 다만 상품들이 크게 카테고리화 되는 느낌이 없는 것 같으니 좀더 세분화해서 분석해볼 필요가 있는 것같다.    


### 또 다른 이슈

1. product id가 숫자로만 이루어진 것이아니다.   
2. 하나의 상품의 가격이 고정되어 있지 않다.    


## 2. TODO

1. 베이스라인 코드 분석   
2. 정형 데이터 학습 알고리즘 조사    
3. 베이스라인 코드 작성
