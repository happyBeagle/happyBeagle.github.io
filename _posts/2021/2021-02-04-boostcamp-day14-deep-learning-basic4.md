---
title: "[BoostCamp] DAY14 Deep Learning Basic#4"
layout: single
author_profile: true
read_time: true
comments: true
related: true
share: true
toc: true
toc_sticky: true
toc_lable: contents
categories:
- BoostCamp_AI_Tech
tags:
- AI_Basics
---

# [BoostCamp] DAY14 Deep Learning Basic#4
---   

## 1. RNN 첫걸음   
### 1) Sequence 데이터란?   
* 소리, 문자열, 주가등의 데이터를 **sequence**데이터라고 한다.    
* Sequence데이너틑 **독립 동등 분포 가정**을 잘 위배하기 때문에 순서를 바꾸거나 과거 정보에 손실이 발생하면 데이터의 확률분포도 달라진다.    


### 2) Sequence 데이터를 다루는 방법!!   
* 이전 sequence정보를 가지고 앞으로 발생할 데이터의 확률 분포를 다루기 위해 조건부 확률을 이용할 수 있다.    
* ![image](https://user-images.githubusercontent.com/68745983/106926945-faf1da80-6754-11eb-862d-fa75dbeeefd1.png)    
* 이를 전개하여 정리해보면 아래와 같은 식을 구할 수 있다.    
* ![image](https://user-images.githubusercontent.com/68745983/106927429-7fdcf400-6755-11eb-87f9-b3854aee24d5.png)   
* 그런데 위의 식을 본다면 t의 크기가 변한 다는 것을 볼 수 있다. 즉, 데이터의 길이가 가변성이 존재한다.   
* 이를 위해서는 **가변적인 데이터를 다룰 수 있는 모델**이 필요하다.    

### 3) Recurrent Neural Network 란?    
우리는 2)에서 배운 식을 아래와 같이 변형시켜 볼 수 있다.    
![image](https://user-images.githubusercontent.com/68745983/106930056-743efc80-6758-11eb-8ca0-5e80ad904315.png)    

이를 모형으로 나타내어 보면 아래와 같이 표현할 수 있다.    
![image](https://user-images.githubusercontent.com/68745983/106930693-2f679580-6759-11eb-9253-b2dc3613f851.png)    

* 그런데 우리는 sequence 데이터를 다루기에 적절한 모델이다. 
* 연속된 데이터를 다루기 위해서는 과거의 데이터를 기억하여 이것또한 학습에 활용할 수 있어야한다.   
* 그렇다면 어떻게 할 수 있을 까?   
	* 위의 식에 과거의 결과값도 추가하여 연산하면 되지 않을 까?   
	* ![image](https://user-images.githubusercontent.com/68745983/106931449-f4199680-6759-11eb-87c0-c9926ff21210.png)  
	* 이를 모형으로 표현해보자.   
	* ![image](https://user-images.githubusercontent.com/68745983/106932178-c41ec300-675a-11eb-952e-9e13e317301a.png)    
	* RNN은 위와 같이 연산할 수 있다. 그렇다면 backpropagation은 어떻게 할 수 있을까?   
	* **BPTT(Backpropagation Through Time)**을 사용해보자.   

### 4) BPTT 란?    
* RNN의 가중치 행렬의 미분을 계산해보자.    
* ![image](https://user-images.githubusercontent.com/68745983/106934442-79527a80-675d-11eb-98ff-4f88c478b6a4.png)   
* 그런데 우리는 여기서 phi연산 부분을 유의 깊게 봐야할 필요가 있다.  
* 활성 함수를 통해 나온 값들을 계속해서 여러번 곱하면 0에 가까워지지 않을까?  
* 해당 부분에 대해 5)에서 이야기 해보도록 하자.    


### 5) 기울기 소실의 해결책은?    
* 일정 길이에서 누적을 끊어 줘보자. 
* 이를 해결하기 위해 나온 것들이 **LSTM**과 **GRU**이다.     

## 2. Recurrent Neural Networks    
### 1) Sequential Model    
### 2) Recurrent Neural Network   
### 3) Long Short Term Memory (LSTM)    
### 4) Gated Recurrent Unit    


## 3. Transformer    


## 4. TODO   
1. 위에서 아직 학습하지 못한 부분에 대해서 복습하며 학습하자.  
2. 아직까지 읽지 못한 논문들이 많다. 읽고 공부하자.   
3. 오늘 학습중 나온 실습 부분을 실습하자.   
4. 코딩 공부를 게을리 하지 말자.   



## 5. 이모저모   

1. 강의   
	* 오늘 역대급으로 어려웠다. 조원분들한테 더 학습할 수 있는 영상을 추천 받았으니 이것도 같이 보면서 학습해야겠다.    
2. 피어세션   
	* 매번 피어세션을 할때마다 조원분들께 많은 것을 배워 가는 것 같다. 항상 감사하다.
