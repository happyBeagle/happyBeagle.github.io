---
title: "[BoostCamp] P-stag Image Classification day2"
layout: single
author_profile: true
read_time: true
comments: true
share: true
toc: true
related: true
toc_sticky: true
toc_label: content
categories:
- BoostCamp_AI_Tech
tags:
- Pstage_Image_Classification
---

# [BoostCamp] P-stage stage1 이미지 분류 day2  
---   

## 오늘의 목표
1. EDA를 해보자.


## 1. EDA

이미지 데이터를 어떻게 EDA해야할지 감이 잡히지 않아 이미지 데이터와 함께 주어진 csv데이터를 EDA하였다.    
csv파일에 주어진 feature는 `age`, `race`, `gender`로 이루어져있었고 나는 여기에 이미지와 csv에서 주어진 데이터를 활용하여 **competition**의 `label`값을 분류하였으며 마스크 착용 유, 무 혹은 오착용여부에 대한 data를 추가해놓았다.   

* ![image](https://user-images.githubusercontent.com/68745983/113173396-4bcd0d80-9284-11eb-8b7a-dd692d266d58.png)   

### feature 통계   
#### gender   

![image](https://user-images.githubusercontent.com/68745983/113174048-f7765d80-9284-11eb-8bb5-6489741c1256.png)   

* 주어진 데이터에서 여성의 수가 남성보다 약 1.5배가량 많은 것을 알 수 있다. 이러한 데이터 불균형으로 인해 학습이 제대로 안된다고 판단될 경우 남성 데이터를 augmentation 혹은 지식 증류 기법등을 활용하여 뻥튀기하는 방법에 대해 알아봐야겠다.   

#### race   

![image](https://user-images.githubusercontent.com/68745983/113176622-a7e56100-9287-11eb-88fe-a860d3edc5d8.png)   

* 주어진 데이터는 모두 아시아인으로 구성되어 있다.    

#### age   

![image](https://user-images.githubusercontent.com/68745983/113177369-673a1780-9288-11eb-855b-0b8cc092153f.png)    

* 여기서 나이는 아래의 기준으로 young, middle, old로 나뉜다.   
	* young < 30
	* 30 <= middle < 60
	* 60 <= old   
* old에 속하는 data가 다른 두 class에 비해 현저히 그 수가 적다. 

##### mask   

![image](https://user-images.githubusercontent.com/68745983/113177287-4ffb2a00-9288-11eb-968c-72a58b5d805f.png)

* 마스크를 착용한 데이터가 마스크를 잘못 착용하거나 착용하지 않은 데이터에 비해 아주 많은 양이 있다.   
* 다만, 모든 data가 같은 종류의 마스크를 착용하지 않았을 것이므로 마스크의 모양, 재질 등에도 관심을 가지고 학습을 시켜보아야겠다.    

#### label   

![image](https://user-images.githubusercontent.com/68745983/113177924-0232f180-9289-11eb-82fb-faba9c546e8d.png)    

* 해당 label의 값 class들은 위에서 살펴보았던 `age`, `race`, `gender`, `mask`의 요소들에 의해 구별된 class들이다.   
* class들간의 양의 차가 매우 많이 나는 것으로 봐서 이에대한 대책을 고민해봐야할 듯하다.   
* 해당 문제를 해결한다면 위에서 `gender`, `mask`요소의 불균형과 같은 문제도 해결할 수 있을 것이라 기대한다.   


### 느낀점

* 이미지를 어떻게 EDA 해?라는 의문을 가지며 시행하였던 EDA였다. 사실, 해당 과정은 정형데이터 분석이라고 말해도 무방할 만큼 이미지에 관한 EDA가 전혀 포함되지 않았다.   
* 하지만 예시로 올려주신 EDA내용들을 보며 이미지를 EDA하는 방법에 대해 조금은 알게 된것 같다.  
	* 이미지 데이터의 RGB평균을 계산해보자.   
	* 이미지 크기에 대해 알아보자.   
	* 이미지 데이터의 RGB값의 표준을 계산해보자.   
	* 이미지의 픽셀값의 분포도를 알아보자.    
	* 이미지를 시각화하여 detection을 시도해보자.(Haar cascade를 사용하여 DL을 사용하지 않고 얼굴을 detect할 수 있다.)   
	* 그 외에도 PCA 즉 주성분 준석을 통해 이미지를 파악해보자.    



## 2.  TODO LIST   
1. ~~EDA를 통해 데이터를 분석해본다.~~     
2. Dataset class를 생성한다.    
3. pytorch에서 제공하는 기본 모델들을 활용하여 학습시켜본다.
