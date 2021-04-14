---
title: "[BoostCamp] P-stage stage2 Tabular Classification day3"
layout: single
author_profile: true
read_time: true
comments: null
share: true
related: true
toc: true
toc_sticky: true
toc_label: content
tags:
- Pstage_Tabular_Classification
categories:
- BoostCamp_AI_Tech
---

# [BoostCamp] P-stage stage2 정형 데이터 분류 day3  
---   

## 오늘의 목표

1. AUC Score는 무엇이죠?
2. Random Forest 이해하기


## 1. AUC는 무엇이죠?

* 사실 어제도 다뤘던 주제이다. 그런데 아무리 생각해도 그래서 이게 뭔데?????????라는 생각만 드는 것이다.   
* 정말 답답했다. ROC curve는 어떻게 그려지는것이고,
* 그래서 AUC는 어떻게 측정되는 것인가!!!
* 그러던 중 [단물 같은 블로그]()를 발견하였다. :) 해당 블로그 글과 여러 자료를 토대로 학습한 것을 한번 정리해보려고 한다.    

> | TEST| 모델 예측이 긍정적 | 모델 예측이 부정적|
|:--------:|:--------:|:--------:|
|  **정답이 긍정적**      |     True Positive   | False Negative|
|  **정답이 부정적**      |     False Positive  | True Negative|     

* 자, 그렇다면 예를 들어 생각해보자. ~~(예시는 그냥 내 대뇌망상에서 나온 통계이므로 그냥 보자.)~~   
* **고양이가 지금 내가 들고 있는 츄르를 좋아할 확률을 고양이의 몸무게로 알아낸다고 생각해보자.**    
* | 고양이 몸무게 | 츄르 선호도(T or F) |
|:--------:|:--------:|
|    2kg    |    T    |
| 2.2kg|F|
|2.3kg|F|
|2.5kg|F|
|3.1kg|T|
|3.3kg|T|
|3.5kg|F|
|4.1kg|T|   

* 자 여기서 우리는 2.5kg보다 낮은 몸무게를 가진 고양이는 츄르를 선호하지 않고(F)   
* 2.5kg이상의 몸무게를 가진 고영희는 츄르를 선호한다(T)라고 가정해보자.  ~~고양인 거의 츄르 좋아하지 않나?~~   
* 그러면 이제 해당 기준으로 우리는 TP, TN, FP, FN을 구할 수 있다.   
* | TEST| 모델 예측이 긍정적 | 모델 예측이 부정적|
|:--------:|:--------:|:--------:|
|  **정답이 긍정적**      |     3(TP)  | 1(FN)|
|  **정답이 부정적**      |     2(FP) | 2(TN)|   

* 여기서 우리는 해당 값을 통해 **TPR**과 **FPR**을 구해주면 된다.    
* **TPR** : TP / (TP + FN) = 3 / (3 + 1) = 0.75   
* **FPR** : FP / (FP + TN) = 2 / (2 + 2) = 0.5   
* 그러면 x축은 0.5, y축이 0.75인 부분에 해당 기준에 대한 ROC curve의 점이 찍힌다. 그러면 나머지 기준들에 대해 계산해보며 **ROC curve**를 그려보면 된다.   

### ROC curve를 그려보자.   
![image](https://user-images.githubusercontent.com/68745983/114668007-2a1b5e00-9d3b-11eb-893d-90a1268d2934.png)   

* 위와 같이 ROC curve를 그릴 수 있다.   
* 그렇다면 여기서 AUC는 무엇일까?   


### AUC를 알아보자.   

AUC는 앞서 구한 ROC curve와 X축사이의 면적을 의미한다. 즉, AUC값이 클수록 TPR과 FPR이 커진다는 것을 의미한다.   
그러므로 AUC가 클수록 모델의 정확도가 높아진다.   

* ![image](https://user-images.githubusercontent.com/68745983/114668654-f0972280-9d3b-11eb-96e5-f1d2a7d0cec8.png)   

## 2. Random Forest가 뭐에오?

* Random Forest를 이해하기 이전에 Decision Tree 즉, 의사 결정 트리에 대해 알아보도록 하자.  

### Decision Tree   

스무고개를 해본적 있을 것이다. 해당 Decision Tree는 스무고개와 비슷한 맥락이라고 생각하면 된다.    

![image](https://user-images.githubusercontent.com/68745983/114713397-0b818b00-9d6c-11eb-8a7b-64ae5958d1f5.png)
   

위와 같이 하나하나씩 문답을 해나가면서 결과가 leaf에 도달할 때까지 질문한다.   
그런데, 이렇게 나눠가는 과정을 통해 학습을 하다보면 두가지의 문제가 있는 것 같다.    

1. 계속 세밀하게 하다보면 노드가 어마무시하게 들어난다. ~~위의 예도 3층이니 2^3 - 1, 그러니까 층이 늘어날 수록 노드수가 어마무시하게 늘어남~~   
2. 큰 트리에서 학습을 하다보면 Overfitting이 발생할 우려가 크다.   

그렇다면 이를 해결하기 위한 해결책은 무엇이 있을까?   
대표적인 방법으로는 **Pruning**즉 가지치기가 있다. 데이터를 버리는 것이아니라 하나로 뭉뜽거려 버리는 것이다.  

![image](https://user-images.githubusercontent.com/68745983/114713640-4a174580-9d6c-11eb-81a3-ef3035a2c684.png)   

위와 같이 원래는 유명인에서 yes라는 답을 받았으면 배우냐?라는 질문을 하게 된다 
**하지만**   
**Pruning**을 한다면 그냥 yes를 받은 시점에서 끝난다. 그냥 그것은 유명인이 되버리는 것이다.   
이런식으로 가지치기를 함으로써 **Overfitting**과 **노드 수**의 문제점을 해결할 수 있다.    

### Random Forest   

* 랜덤 포레스트는 단순히 생각해보면 **Decision Tree**의 **Ensemble**이라고 보면 된다.    
* Pruning된 여러 Decision Tree의 결과값을 Ensemble한 것이라고 보면된다.   

#### Bagging 및 학습 과정  

* 랜덤 포레스트에 training input을 넣으면 Bagging의 과정을 거치게 된다.   
* Bagging은 하나의 dataset을 여러 subset으로 만들어 준다.
* subset으로 만들어진 dataset들은 Pruning된 여러 Decision Tree에 넣어서 결과값을 계산한다.   
* 이렇게 나온 결과값을 Ensemble하여 최종 결과를 도출한다.

![image](https://user-images.githubusercontent.com/68745983/114716570-23a6d980-9d6f-11eb-99ea-886a24d7d13a.png)


## 3. TODO

1. 베이스라인 코드 분석   
2. ~~AUC공부하기~~
2. 정형 데이터 학습 알고리즘 조사    
3. 베이스라인 코드 작성
