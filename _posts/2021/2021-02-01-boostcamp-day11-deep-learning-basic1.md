---
title: "[BoostCamp] DAY11 Deep Learning Basic#1"
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- BoostCamp_AI_Tech
tags:
- AI_Basics
toc: true
toc_sticky: true
toc_label: contents
---

# [BoostCamp] DAY11 Deep Learning Basic#1
---   

## 1. 베이즈 통계학   
베이즈 통계학을 이해하기 위해선 조건부확률의 개념을 이해해야한다.    

### 1) 조건부 확률
![image](https://user-images.githubusercontent.com/68745983/106435878-c3660280-64b6-11eb-8a58-cd8b4dfe9805.png)  
**사건 B가 일어난 상황에서 사건 A가 발생할 확률을 의미한다.**   
* 베이즈 정리는 조건부 확률을 이용하여 **<span style="color:orange">정보를 갱신하는 방법</span>**을 알려준다.   
![image](https://user-images.githubusercontent.com/68745983/106436242-353e4c00-64b7-11eb-9359-860251b4c82f.png)   
* 즉, B라는 정보가 주어졌을 때 P(A)로부터 P(A\|B)를 계산하는 방법을 제공한다.    

### 2) 베이즈의 정리    
![image](https://user-images.githubusercontent.com/68745983/106437509-b21df580-64b8-11eb-8807-7019d7652e2c.png)   
* **사후확률** : 데이터가 주어졌을때 해당 parameter가 성립할 확률   
* **사전확률** : 데이터가 주어지기전 현재 가지고 있는 정보로 정해지는 주관적으로 판단내린 확률   
* **증거** : 데이터 자체의 분포   
* **가능도** : 현재 주어진 데이터에서 data가 관찰될 확률   
* **D** : data   
* **θ** : 모수   

#### 조건부 확률의 시각화    
![image](https://user-images.githubusercontent.com/68745983/106449590-73dc0280-64c7-11eb-9e51-580762ab972d.png)   

### 3) 베이즈 정리를 통한 정보의 갱신    
* 베이즈 정리를 통해 새로운 데이터가 들어왔을 때 **앞서 계산한 사후 확률을 사전 확률로 사용하여 <span style="color:orange">갱신된 사후 확률을 계산</span>**할 수 있다.   
![image](https://user-images.githubusercontent.com/68745983/106450142-257b3380-64c8-11eb-80b3-fdfec863814f.png)    

### 4) 조건부확률 -> 인과관계?    
* 조건부 확률은 유용한 통계적 해석을 제공하지만 **<span style="color:orange">인과관계</span>**를 추론할 때 함부로 사용해서는 안된다.   
* 데이터가 많아져도 조건부 확률만 가지고 인과관계를 추론하는 것은 불가능하다.   
* 인과관계는 데이터 분포의 변화에 강건한 예측모형을 만들때 필요하다.
	* 단, 인과관계만으로는 높은 예측 정확도를 담보하기는 어렵다.
* 인과관계를 알아내기 위해서는 **<span style="color:orange">중첩요인의 효과를 제거</span>**하고 원인에 해당하는 변수만의 인과관계를 계산해야한다.   

## 2. Deep Learning Basics_Historical Review    
이번 강의에서는 해당 카테고리의 강의를 통해 무엇을 배울지 알려주시면서 **Denny Britz의 <span style="color:orange">Deep Learning's Most Important Ideas - A Brief Historical Review</span>라는 논문**에 기반하여 딥러닝의 역사에 대해 배울 수 있었다.   
### 1) Key Components of Deep Learning   
* The **data** that the model can learn from   
	* 데이터는 해결해야하는 문제의 유형에 의존한다.   
* The **model** how to transform the data   
	* ex) AlexNet, GoogleNet, ResNet, DenseNet... 
* The **loss** function that quantifies the badness of model   
	* loss function is a proxy if what we want to achieve  
* The **algorithm** to adjust the parameter to minimize the loss   
	* 최적화를 위한 알고리즘  

### 2) Historical Review   
#### 2012년   
**AlexNext**   
ImageNet 영상 데이터 베이스를 기반으로 한 화상 인식 대회인 **ILSVRC 2012**에서 우승한 CNN구조이다.   
<span style="color:orange">GPU를 기반으로한 2개의 병렬구조</span>로 구성되었다는 점이 눈여겨 볼만하다.   
[관련 논문](https://papers.nips.cc/paper/2012/file/c399862d3b9d6b76c8436e924a68c45b-Paper.pdf)    

#### 2013년   
**DQN**   
Deepmind에서 작성한 논문인 <span style="sykblue">Playing Atari with Deep Reinforcement Learning</span>에서 Q함수를 이용한 **Q-Learning**에 Deep Learning을 결합하여 Atari 2600의 고전 게임을 성공적으로 플레이하는 에이전트를 발표하였다.   
[관련 논문](https://arxiv.org/pdf/1312.5602.pdf)   

#### 2014년   
**Encoder/Decoder**   
Encoder과 Decoder는 각각 RNN으로 구현되면 단뒤정보는 Word Embedding을 통해 Continuous Value로 변환되어 사용된다.   
현재에는 Sequence-Sequence(seq2seq)라고도 한다.   
[관련 논문](https://arxiv.org/pdf/1409.3215.pdf)     

**Adam Optimizer**   
목적함수 f의 최솟값을 찾는 최적화 알고즘의 한 종류이다.   
Momentum + RMSProp의 기본아이디어를 합친 알고리즘이다.   
step size가 gradient의 rescaling에 영향을 받지 않는다는 장점이 있다. 즉, gradient가 커져도 stepsize는 bound가 되어있어서 어떠한 object function을 사용한다 하더라도 안정적으로 최적화를 위한 하강이 가능하다.   
[관련 논문](https://arxiv.org/pdf/1409.3215.pdf)   

**Generative Adversarial Network**   
우리나라 말로 **생성적 적대 신경망**이라고 하며 줄여서 **<span style="color:bule">GAN</span>**이라고 한다.  
비지도학습에 사용되는 인공지능 알고리즘으로 제로섬게임 틀안에서 서로 경쟁하는 두개의 신경 네트워크 시스템에 의해 구현된다.   
[관련 논문](https://arxiv.org/pdf/1406.2661.pdf)    

#### 2015년   
**Residual Networks**   
2015년 ILSVRC에서 우승한 모델이다.   
기존에 deep learning에서 깊은 층으로 이루어져 학습을 진행할 수록 **정확도가 줄어드는 문제**가 있었다. 하지만 ResNet의 개발로 인에 기존의 7배(152층)이 되는 층에서 현저히 높은 성능을 보이며 그 우수성이 입증되었다.   
[관련 논문](https://arxiv.org/pdf/1512.03385.pdf)   

#### 2017년   
**Transformer**   
2017년 구글에서 발표한 논문인 **<span style="color:skyblue">Attention Is All You Need</span>**라는 논문에서 나온 모델이다. 기존의 seq2seq구조를 따르면서 attetion만으로 구현이 되었다. RNN보다 우수하다는 특징을 가지고 있다.   
[관련 논문](https://arxiv.org/pdf/1706.03762.pdf)    

#### 2019년    
**Bert(fine-tune NLP models)**   
구글에서 개발한 NLP 사전 훈련기술이다, 특정분야에 국한된 기술이아니라 **모든 자연어 처리 분야에서 좋은 성능을 내는 범용 Language model**이다.   
[관련 논문](https://arxiv.org/pdf/1810.04805.pdf)    

**Big Language Models**   
OpenAI가 개발한 새로운 강력한 언어모델이다.(GPT-3)    
[GPT-3](https://arxiv.org/pdf/2005.14165.pdf)    
[GPT-2](https://d4mucfpksywv.cloudfront.net/better-language-models/language_models_are_unsupervised_multitask_learners.pdf)    
[GPT-1](https://s3-us-west-2.amazonaws.com/openai-assets/research-covers/language-unsupervised/language_understanding_paper.pdf)    

#### 2020년   
**Self supervised Learning**   
일반적으로 지도학습이 높은 성능의 모델을 만드는 것이 유리하자, 하지만, 수 많은 데이터에 label을 달아야한다는 점, 신뢰성 있는 데이터의 수집 등 다양한 어려움들로 인해 활용하는데 제한이 존재한다.   
이를 해결하기위해    
* 아주 일부만 존재하는 label이 존재하는 dataset을 활용하는 semi-supervised learning    
* label이 전혀 없는 dataset을 활용하는 unsupervised learning   
등을 활용한다.    
그런데 최근에는 **자기지도 학습이 주목 받고 있다.** (다음에 기회가 된다면 알아보자.)    

[관련 블로그 1](https://velog.io/@tobigs-gm1/Self-supervised-learning-paper-review)   
[관련 블로그 2](https://greeksharifa.github.io/self-supervised%20learning/2020/11/01/Self-Supervised-Learning/#self-supervised-learning)


## 3. Deep Learning Basics_Neural Networks & Multi-Layer Perceptron    
### 1) Neural Network?  
```   
Neural Network는 동물의 뇌에 있는 생물학적 뉴런 체계에 영감을 얻어 개발된 Computing System이다.
```   
#### Linear Neuar Networks  
![image](https://user-images.githubusercontent.com/68745983/106457863-f5855d80-64d2-11eb-9558-6cb0db41aefb.png)   
위와 같이 아주 간단한 선형 회귀를 생각해보자. 여기서 우리는 loss값을 미분하여 극솟값을 찾을 수 있다.   
W, b에 대해 각각 미분하여 알맞은 W, b를 찾아보자.   
![image](https://user-images.githubusercontent.com/68745983/106458115-409f7080-64d3-11eb-9064-f05e04b397e7.png)   
우리는 W를 Matrix로 변형시켜 보다 간단하게 X의 종류가 여러개인 경우의 문제를 해결할 수 있다.   
그런데, 이렇게 만들어진 선형회기를 여러 층으로 쌓아 두면 Neural Network라고 할 수 있을 까?

##### Linear block을 여러 층을 쌓게 되면 Neural Network라고 할 수 있을 까?   
**<span style="color:red">아니다!!!!!</span>**   
무작정 층을 쌓게 된다면 결국, 그것은 하나의 linear block이 된다.   
우리는 하나의 block을 통과한 값을 활성화 함수를 통해 변형시킨 후, 다음 layer에 전달해야한다.   

> 활성화 함수로는 ReLU, sigmoid등이 존재한다.   

### 2) Multi-Layer Perception (MLP)   
두 층이상의 Neural Network가 쌓인것을 **MLP**라고 한다.   
![image](https://user-images.githubusercontent.com/68745983/106458756-2fa32f00-64d4-11eb-9a34-55062c1989fc.png)


## 4. Pytorch Basics
[Pytorch로 시작하는 딥러닝 입문](https://wikidocs.net/book/2788)을 통해 공부해보자.   

## 5.TODO   
1. 2-2)의 논문 공부하기   
2. 나만의 dataset class구현해보기    


## 6.그외 이모저모   
1. 강의  
- 이제까지 인공지능을 배우기 위한 초석을 다졌다면, 오늘부터 인공지능을 위한 첫 걸음마를 시작한 것같다.   
- 앞으로 더 열심히 해서 잘 할 수 있도록해야겠다. 
2. 피어 세션  
- 오늘 들었던 강의리뷰에서 각자 중점을 두고 본것이 다르다는 것에 놀랬다.
- 강의리뷰 외에도 학습교재, 팁등에 대해서 이야기를 나누었는데, 많은 도움을 받은 것 같아 감사했다.
