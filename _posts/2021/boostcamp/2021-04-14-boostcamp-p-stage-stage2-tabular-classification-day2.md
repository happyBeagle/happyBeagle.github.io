---
title: "[BoostCamp] P-stage stage2 Tabular Classification day2"
layout: single
author_profile: true
read_time: true
comments: null
share: true
related: true
toc: true
toc_sticky: true
toc_label: contents
tags:
- Pstage_Tabular_Classification
categories:
- BoostCamp_AI_Tech
---

# [BoostCamp] P-stage stage2 정형 데이터 분류 day2  
---   

## 오늘의 목표

1. EDA를 해보자.
2. AUC Score는 무엇이죠?

## 1. EDA

* 어제 했던 EDA파일이 다 날아갔다. ~~인생, 제대로 된다하면 제대로 되지 않는다~~
* 그래서 새로 EDA를 했다.   
* 그런데 어제 EDA가 약간 개판이라는 걸 깨달았다. ~~날아간게 다행인가..?~~   
* 그래서 새로운 마음으로 다시 시작해보자. ~~이번주는 이론 공부하면서 EDA만 할꺼임 아무튼 그럴꺼임~~   

### 처음부터 다시 시작

#### order id    

이번에는 주문 번호에 따른 데이터를 확인을 먼저 해보았다.    

1. 매월 주문 건수는 어떻게 될까?   
	* ![image](https://user-images.githubusercontent.com/68745983/114574439-37413a00-9cb4-11eb-913b-d569180a0d8b.png)
	* 11월에 주문 건이 매우 느는 것을 확인할 수 있다. ~~겨울 나기 준비인가?~~    
	* 그에 반에 12월에는 주문 량이 11월에 비해 뚝. 떨어진다. ~~배송지연?? 아닌데 주문이니 12월에도 가능할 것같은데 왜죠?~~    
	* 이를 겹쳐서 한번 확인해보자.
	* ![image](https://user-images.githubusercontent.com/68745983/114578476-dd427380-9cb7-11eb-9f31-d1e21a2799b7.png)  
	* 모양이 비슷하다. 그렇다면 매년 비슷하다는 시각으로 접근해보는 것도 좋을 것같다.

2. 매월 주문 금액은 어떻게 될까?
	* ![image](https://user-images.githubusercontent.com/68745983/114575652-58eef100-9cb5-11eb-95c4-ec5cb7c423d3.png)    
	* 크게 변화되는 건 없어보인다.    
	* 굳이 보면 2010년 4월 구매품목이 꽤 비싼것 인것 같다. 5월과 꽤 비슷하다   
		* ~~근데 5월이 싼거일 수 있음~~    
	* ![image](https://user-images.githubusercontent.com/68745983/114579305-b2a4ea80-9cb8-11eb-9257-a8e42a59eabc.png) 
	* navy색이 2011년이다.   
	* 매년 구매 금액이 비슷한 양상을 보이고 있는 것으로 생각된다. 이를 유념하며 학습을 시켜도 될것같다.   
3. 고객들의 주문 패턴을 탐색해보자.   
	* ![image](https://user-images.githubusercontent.com/68745983/114579706-15968180-9cb9-11eb-84af-25198cdbd8af.png)  
	* 13777고객을 본다면 매년 구매 패턴이 반복되는 것을 확인해볼 수 있다.   
	* 다른 고객들의 구매 양상을 확인해보고 이를 생각해서 학습 데이터를 꾸려 보자.   

#### product id   

강의에서 강사님이 product_id를 처음 3개의 문자 만을 가지고 와서 카테고리화 하는 것을 보여주셨다.   
일부의 데이터만을 보여줘서 모든 데이터를 확인해보기로 하였다.    

1. 각 카테고리는 어떤 제품을 포함하고 있을까?   
	* ![image](https://user-images.githubusercontent.com/68745983/114580608-f5b38d80-9cb9-11eb-9385-fa57f3e4d65a.png)    
	* 850: 양초, 사탕, 점박이, 그릇, 세트 뭔가 잡화에 관련된 제품이 포함된 것같다. 더불어 set의 글자 크기가 가장 큰것으로 봐서 세트 상품으로 주로 구성된 제품들이 포함되어 있지 않을까 생각된다.    
	* 793: 테이블, 꽃, 램프, 라이트 뭔가 테이블위에 올려놓고 인테리어를 할것 같은 제품들이 모여 있는 것같다.   
	* 220: 티슈, 카드, 생일, 박스 등 파티와 관련된 제품들이 아닐까 생각한다.   
	* ![image](https://user-images.githubusercontent.com/68745983/114581743-f13ba480-9cba-11eb-9777-d83015afa0f3.png)   
	* 212: 가랜드, 초, 접시 등 이것도 파이 용품으로 추측된다.   
	* 218: 머그, 종, 크리스마스,,, 크리스마스 용품인가...?
	* 215: 튜브, 다이어리, 레트로...흠... 어렵다 모르겠다.    
	* ![image](https://user-images.githubusercontent.com/68745983/114582469-93f42300-9cbb-11eb-9822-ae1dcb90669e.png)   
	* 150: 정원 제품인거로 보인다. ~~파라솔이 강력하다~~   
	* 460: 사이즈가 나오고 폴리에스터가 나오는걸로 봐서는 천이아닐까 생각이 된다.   
	* 844: 메탈, 쿠션, 토끼, 치킨, 보석 뭔가 잡화에 관련된 제품들 아닐까 생각해본다.   
	* ~~더는 못하겠다 카테고리가 약 120개가 되는데 이거 다하고 나면 눈이 빠질것 같다 나머지는 필요할때마다 꺼내오도록 하겠다.~~   
2. 카테고리별 월별 판매량   
	* ![image](https://user-images.githubusercontent.com/68745983/114583206-53e17000-9cbc-11eb-9ede-a1f090739183.png)    
	* M은 +로 가지를 않는다. 뭔가 하자가 있을 때 고객을 대응할때 사용되는 금액인것 같다. ~~합의금인가??~~   
	* ![image](https://user-images.githubusercontent.com/68745983/114584958-1bdb2c80-9cbe-11eb-8788-b91be2ae8f3e.png)   
	* ~~200번대는 다시봐도 더럽다~~
	* 그래도 10월 ~11월 사이에 구매금액이 증가하는 패턴을 파악할 수 있었다.
	* 다만 300번대의 제품들 중에는 유행을 타는 제품들이 존재하는 것같다. ~~날이 갈수록 구매를 안함~~   
	* ![image](https://user-images.githubusercontent.com/68745983/114585319-7c6a6980-9cbe-11eb-81b8-a4cd55604120.png)    
	* 400번대는 음...위에 구매량이 서로 정반대인 두 제품빼고는 없는건가...? 구매율이 저조하네.   
	* ~~어차피 티끌모아 티끌이라 없애도 될듯하다.~~    
	* 500번은 뭔가 구매량을 대표해서 보여주는 것같다.    
	* ![image](https://user-images.githubusercontent.com/68745983/114585601-c6ebe600-9cbe-11eb-91d6-81ad17f08bcb.png)   
	* 600번대는 정말 자유롭게 쓰여지는 것같다.   
	* 700번대 제품하나는 보이콧 당한건가 엄청 반품이 들어왔다. ~~옥X크X?~~   
	* ![image](https://user-images.githubusercontent.com/68745983/114585831-031f4680-9cbf-11eb-9f98-460377be03b6.png)   
	* 800번대 제품에서도 살릴것과 탈락시킬 제품을 파악할 수 있다.   
	* 900번대 제품은 지멋대로인듯하면서 다른 제품들과 비슷한 양상으로 구매되어 지는 것으로 보인다.   

##### PLUS   
* Product id를 보면 전혀 제품을 의미하는 것같지 않는 요소들이 보이기도한다.   
* 그런 요소들을 제외하고 학습을 시키면 어떨까?   
* 그래서 해당 요소들을 제외하고 test set의 customer id와 train set의 customer id의 차를 보았다.  
* test set의 60명이 train set에 포함되어 있지 않다.   
* 해당 부분을 어떻게 할지 고민을 해봐야겠다.    


## AUC가 뭐에요??   

이번 stage의 채점 점수 기준은 AUC라고 하였다. 그러면 AUC가 무엇일까? 알아보자.   

### 용어 정리 

#### TP, TN, FP, FN    


| TEST| 모델 예측이 긍정적 | 모델 예측이 부정적|
|:--------:|:--------:|:--------:|
|  **정답이 긍정적**      |     True Positive   | False Negative|
|  **정답이 부정적**      |     False Positive  | True Negative|   

#### ROC curve?   

curve를 표현하는데에는 그래프만큼 좋은 도구가 없다. 그렇다면 ROC를 알아보기 위해서 각각 축들에 대해 이해하고 넘어가보자.   

**X 축은 FP의 비율을 나타낸다. 즉 (FP의 수들의 합) / (정답이 Negative의 수들의 합)이 된다.**
* 이는 negative한 정답들 중 모델이 positive라고 잘못 예측한 비율이라고 보면 된다.   

**Y 축은 TP의 비율을 나타낸다. 즉 (TP의 수들의 합) / (정답이 Positive의 수들의 합)이 된다**   
* 이는 정답이 Positive인것들중 정답을 제대로 맞춘것들의 비율을 말한다.   


### AUC   

* AUC는 여기서 ROC가 X축과 가지는 면적을 의미한다.   
* ![image](https://user-images.githubusercontent.com/68745983/114588947-2d263800-9cc2-11eb-99c0-7b446ecbc8a0.png)
* > 출처 : https://developers.google.com/machine-learning/crash-course/classification/roc-and-auc?hl=ko   
* 아직 이해가 잘가진 않는다 다시 이해해보고 와서 설명을 배봐야겠다. 






## 2. TODO

1. 베이스라인 코드 분석   
2. AUC공부하기
2. 정형 데이터 학습 알고리즘 조사    
3. 베이스라인 코드 작성
