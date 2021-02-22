---
title: "[BoostCamp] DAY18 NLP#3"
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- BoostCamp_AI_Tech
tags:
- NLP_basic
toc: true
toc_sticky: true
toc_label: contents
---

# [BoostCamp] DAY18 NLP#3
---   

## 1. Sequence to Sequence with Attention    
### 1) Seq2Swq with attention Encoder-Decoder architecture Attention Mechanism    
* 연속된 단어를 input으로 받고 연속된 단어를 output으로 받는다.    
* hidden state : encoder에서 받은 단어들을 저장해두고 Decoder에 전달함    

<p align="center"><img src="https://user-images.githubusercontent.com/68745983/108152017-6d7e9500-711b-11eb-8289-01f09d7eb424.png" /></p>    


#### Attention Model    

**Problem?**   

* hidden state vector에 sequence 전체의 정보를 축적하고 있어야한다.   
* LSTM에서 Long-Term dependency가 해결되었다하더라도 정보의 소실, 왜곡들이 일어날 가능성이 있다.   
* 초반에 나온 단어의 정보의 유실 가능성이 있다.   
	* 이를 해결하기 위해 문장을 뒤집어서 사용해보자. --> 초반의 단어는 학습이 보다 잘될것이다.   

**Attention Problem SEtting**   

* Decoder는 Encoder의 마지막에 나온 hidden state vector를 활용할 뿐만아니라 Encoder 중간 중간의 hidden state vector 도한 활용하자.    
* Decoder는 각 timestep마다 번역을 할때 그때마다 필요한 hidden state vector를 가져와서 활용하자.   
* 

##### Attention Module의 동작 과정    
1. 아래의 그림과 같이 프랑스어를 번역하는 과정을 예로 생각해보자.   
	* ![image](https://user-images.githubusercontent.com/68745983/108152493-7fad0300-711c-11eb-8f57-da0cb066550c.png)   
	* Encoder에서 생성된 마지막에 생성된 hidden state vector 즉, h₄가 Decoder에서는 h0로 입력이 된다.   
	* 또한 STATR Token으로 주어지는 값이 input값으로 들어 가게 될것이다.   
	* 여기서 이제 Decoder의 hidden state vector가 생성되는데 h0와 start token을 통해 생성된 h1은   
		* 다음 단어의 예측에 사용된다.  
		* Encoder에서 주어진 hidden state vector들중 어떤 것들을 필요로하는지 선정을 하게 된다.   
2. 이제 Decoder의 hidden state vector에서 필요로하는 Encoder의 hidder state vector를 구해보자.   
	* ![image](https://user-images.githubusercontent.com/68745983/108153009-a28be700-711d-11eb-8da0-4fb4f31690e3.png)   
	* Decoder의 hidden state vector와 Encoder의 hidden state vector를 내적시켜 유사도를 검사한다.   
		* 내적값이 높을 수록 유사도가 높다고 판단한다.   
	* 해당 결과 값들을 softmax에 통과시켜 확률 값을 계산해준다.   
3. softmax의 각각의 결과 값은 각각 연관된 Encoder의 가중치로써 사용이 된다.   
	* ![image](https://user-images.githubusercontent.com/68745983/108153383-65742480-711e-11eb-85fe-94282d71377d.png)   
	* 여기서 구해진 가중치들을 각각의 Encoder hidden state와 곱하여 가중 평균을 구할 수 있다.    
	* 이를 통해 Attention output을 구할 수 있다.   
	* ![image](https://user-images.githubusercontent.com/68745983/108153697-05ca4900-711f-11eb-8136-ebdcd64f407a.png)    
4. 이제 여기서 구해진 Attention Model의 결과를 활용하자.   
	* Decoder의 output과 Attention Model의 output을 concat하여 예측값을 계산한다.    
	* ![image](https://user-images.githubusercontent.com/68745983/108153839-4cb83e80-711f-11eb-94b1-e9da3f3b5fee.png)     
5. End Token이 나올때까지 2~4 작업을 반복한다.    

> Teacher Forcing
> 학습이 더빨리 진행된다.   
> 다만 실제 상황에서는 괴리가 발생한다.   
> 모델 초반 Teacher forcing 이후에 사용X   

**유사도를 구하는 방법**  
![image](https://user-images.githubusercontent.com/68745983/108154763-dfa5a880-7120-11eb-88d6-6205e0a7549a.png)    


##### Attention의 장점    
1. Attention이 Seq2Seq에 추가되면서 기계번역의 성능을 매우 향상시켰다.    
	* Decoder의 매 입력마다 어떤 부분의 정보를 집중해서 사용할까?    
2. bottleneck problem해결   
3. Gradient Vanishing문제 해결을 할 수 있다.    

## 2. Beam Search   

* Seq2Seq with Attention은 Greedy Decoding방법을 사용한다.
	* ** Greedy Decodiing**   
	* 전체적인 문장의 확률을 보는 것이 아니라 근시안적으로 높은 확률 가진 단어를 선택한다.    
* 해당 방법을 사용하면 중간에 잘못된 판단을 하였음에도 이를 수정할 수 있는 방법이 없다.    
* **어떻게 이를 해결할 수 있을까?**   
	* ![image](https://user-images.githubusercontent.com/68745983/108156245-9e62c800-7123-11eb-8cc1-170cd8310a27.png)   
	* 입력 문장을 x, 출력 문장을 y라고 했을때 주어진 문장 x에 대한 출력 문장 y의 확률 분포를 위와 같이 구할 수 있다.   
		* timestep t까지의 가능한 경우를 모두 고려한다고 봤을 때
		* 시간 복잡도는 O(V^t)이다.
		* **매우 값이 급격히 커질테고 비효율 적이다.**   
	* 차선책으로 우리는 Beam Search를 사용하여 학습할 수 있다.   

### Beam Search Core Idea   

* Greedy + 모든 경우의 수를 고려하는 방법의 중간 쯤 존재한다.   
* K개의 가능한 가지수를 고려하여 가장 높은 확률을 가진 값을 선택한다.  
	* K : beam size (주로 5 \~10 )   
* ![image](https://user-images.githubusercontent.com/68745983/108157000-18478100-7125-11eb-88ee-942a0ecd8363.png)

* **가장 좋은 방법을 찾는다라고는 보장하지 않는다.**    
* **하지만 모든 경우를 따져서 계산하는 것보다 더 효율적으로 계산이 가능하다.**    

### Beam Search Example   

<p align="center"><img src="https://user-images.githubusercontent.com/68745983/108157758-d4557b80-7126-11eb-9452-580cae40c2fb.png" /></p>
 
* 각각의 timestep에서 높은 확률을 가지는 k개의 word를 선택하여 해당 word의 다음에 나올 word를 계산한다.    
* 그 다음에도 k개의 word를 선택해서 다음에 올 word를 계산한다.   

### Beam Search가 끝나는 시점   

* 우선, END token을 출력한 문장은 memory에 저장해 놓는다.   

1. timestep에 제한을 두어 timestep이 제한을 넘기면 멈춘다.    
2. memory에 저장된 문장의 수에 제한을 두어 원하는 양의 문장이 모였을 경우 학습을 멈춘다.    


### 결과 값을 return하자.   

* 가장 높은 확률을 가진 값을 return하자   
* ![image](https://user-images.githubusercontent.com/68745983/108158245-e1269f00-7127-11eb-9049-0b23e5cbda8e.png)    
* 다만, 긴 문장일 수록 확률값이 작아지는 문제를 해결하기 위해 정규화를 시켜 보는 것은 어떨까?   
* ![image](https://user-images.githubusercontent.com/68745983/108158272-ef74bb00-7127-11eb-8a1f-f77e4396fe54.png)    

## 3. BLEU score   

* 우리가 이제까지 배운 Encoder, Decoder는 어떻게 그 성능을 책정할 수 있을까?   

### Precision and Recall   

예제를 들어 **<span style="color:orange">Precision</span>**과 **<span style="color:orange">Recall</span>**에 대해 알아보자.    

* Reference : <span style="color:green">Half</span> of <span style="color:green">my heart is in</span> Havana <span style="color:green">ooh na</span> na    
* Predicted : <span style="color:green">Half</span> as <span style="color:green">my heart is in</span> Obama <span style="color:green">ooh na</span>    

두 문장에 나타난 word를 고려했을 때 <span style="color:green">초록색</span>으로 표시된 부분이 알 맞게 예측된 부분인 것을 알 수 있다.   
여기서 **Precision**과 **Recall**을 구해보자.    

![image](https://user-images.githubusercontent.com/68745983/108235724-76a64b00-7189-11eb-9d80-c2dc74e41d79.png)    

해당 식을 보면 **Precision은 <span style="color:orange">예측값에 초점</span>**을 두고 **Recall은 <span style="color:orange">참조값에 초점</span>**을 두는 것을 알 수 있다.

* **Precision**   
	* 정밀도란 모델이 참이라고 판단한 것들 중 실제로 참인것을 의미한다.   
	* Positive 정답률이라고도 한다.    
* **Recall**   
	* 재현율이란 실제 참인 것들 중 모델이 참이라고 판단한 것의 비율이다.    
	* 통계학에서는 *Sensitivity*라고 하며 다른 분야에서는 *hit rate*라고도 한다.   
* **Recall과 Precision은 True인 정답이 모델이 True라고 예측하는 경우에 관심을 가지지만, 관점이 다르다.**   
* 그렇다면 Recall과 Precision을 적절히 조합하여 모델의 정확도를 계산할 수 있지 않을 까?    
	1. 평균을 내보자.   
		* ![image](https://user-images.githubusercontent.com/68745983/108238752-968b3e00-718c-11eb-830f-d22dcc3f2679.png)    
		* 각각의 평균 값들 중 상황에 따라 적합한 방법을 선택하여 연산하면 된다.   


#### Problem   

해당 예측방법은 anagram처럼 같은 word의 집합을 가지나 순서가 다른 문장을 만들어 냈을 때 정확도가 100%라는 결과 값을 가진다.   
그렇다면 이를 해결하기 위해선 어떻게 해야할 까?    

### BiLingual Evalution Understudy (BLEU)    
*  model의 결과 값인 output값과 기댓 값인 reference 문장을 **<span style="color:orange">N-gram overlap</span>**의 방식으로 비교해보자.   
* 1~4의 n-gram을 통해 **Precision**을 계산하자.   
* 또한 recall을 고려하기 위해 **Brevity panalty**를 구해주자.
	* 이는 너무 짧은 결과 값을 위해서도 적용된다.   
* ![image](https://user-images.githubusercontent.com/68745983/108239968-bec76c80-718d-11eb-8630-c9b6ce00ae3d.png)   

> **n-gram?**
> 문장의 word를 연속된 n개로 묶어 서로 비교를 하는 것   
> 예) 나는 배가 고프다.을 2-gram으로 나누면,    
> 1. 나는 배가   
> 2. 배가 고프다.   
> 로 나뉘어 질 수 있다.    

* 위의 n-gram방법으로 문자열을 비교하면 동일한 문자로 이루어진 순서가 다른 문장을 다른 것으로 인식할 수 있다.   


## 3. Plus Question   

* 1.BLEU score가 번역 문장 평가에 있어서 갖는 단점은 무엇이 있을까요?


## 4. 이모저모   

1. 강의   
	* 오늘은 자연어 처리 model뿐만아니라 그 성능을 평가하는 방법에 대해서도 학습하였다.   
	* 다양한 것들을 알게 되었는데 조금 더 넓고 깊게 볼 수 있도록 복습을 해야겠다.   

2. 피어세션   
	* 서로 보는 시각이 달라 다양한 부분에 대해 이야기를 나누었다.   
	* 하지만 각각의 부분에 대해 아직 이해가 미흡한 것 같아 피어세션에서 나온 주제들에 대해 다시 복습할 수 있는 시간을 가져보아야겠다.  
3. 마스터 세션   
	* 평소 NLP에 관해 궁금했던 부분에 대해 알 수 있어 값진 경험이었던 것 같다.
