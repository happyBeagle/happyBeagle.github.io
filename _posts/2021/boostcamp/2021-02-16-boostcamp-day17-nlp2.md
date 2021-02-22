---
title: "[BoostCamp] DAY17 NLP#2"
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- BoostCamp_AI_Tech
tags: []
toc: true
toc_sticky: true
toc_label: contents
---

# [BoostCamp] DAY17 NLP#2
---   

## 1. RNN and Language Model    
### Types of RNN  
#### - One-to-one  
입출력이 하나인 경우를 말한다.   
<p align="center"><img src="https://user-images.githubusercontent.com/68745983/108009049-258d3e80-7045-11eb-996a-72c6fef062eb.png" /></p>    

sequential, timestamp로 이루어진 데이터가 아닌 단일한 데이터로 input, output을 사용한다.   

#### - one-to-many   
<p align="center"><img src="https://user-images.githubusercontent.com/68745983/108009262-a815fe00-7045-11eb-8c02-6db1b090c615.png" /></p>    

sequential, timestamp로 이루어 지지 않은 단일한 input data로 sequential한 output을 가지고 오는 경우를 말한다.   
* ex) Image Captioning     

> sequential한 데이터를 input으로 입력해야하는 경우, 나머지 input은 0으로 입력해주면 된다.   


#### - many-to-one   
<p align="center"><img src="https://user-images.githubusercontent.com/68745983/108009590-66d21e00-7046-11eb-8a88-97aa6f3956ae.png" /></p>   

sequential한 data를 input으로 받은 후에 최종 결과를 마지막 step에 return 해주는 경우를 말한다.   
* ex) Sentiment Classification   

#### - many-to-many   

* **first case**      

<p align="center"><img src="https://user-images.githubusercontent.com/68745983/108009899-0099cb00-7047-11eb-972a-f2599f7bbd21.png" /></p>     

input을 다 읽은 후 output을 return 해준다.     
* ex) machine translation    
	
* **second case**     

<p align="center"><img src="https://user-images.githubusercontent.com/68745983/108010021-540c1900-7047-11eb-8a41-dc4b97eb60ee.png" /></p>       

input이 주어질 때마다 output을 return 하는 형태도 존재한다. (실시간 성이 필요한 경우)     
* ex) video classification on frame level

### Character level Language Model   
**언어 모델?**   
주어진 문자열, 단어 순서를 기반으로 다음 단어를 예측하는 것을 Task    

#### How to training?   
1. character level의 사전을 구축한다.   
	* 각각의 chatacter를 one-hot vector로 표현이 가능하다.    
2. 단어가 주어지면, 주어진 단어를 character 단위로 쪼개어 입력할때, 다음에 나올 charater를 예즉하는 output이 나올 수 있도록한다.   
	* ![image](https://user-images.githubusercontent.com/68745983/108010534-70f51c00-7048-11eb-874c-4119f624c190.png)   
	* 그림과 같이 hello라는 단어를 character단위로 쪼개어 본다면 h, e, l, l을 순서로 input이 입력되게 된다.   
	* 그러면, 우리는 h가 입력됐을 때 e가 반환되고   
	* e가 입력됐을 때 l이 반환되는 model을 기대한다.   
3. input들은 RNN의 hidden layer를 통해 training을 한다.   
	* ![image](https://user-images.githubusercontent.com/68745983/108010744-ed87fa80-7048-11eb-84db-5fcdbdf52ed1.png)    
	* ![image](https://user-images.githubusercontent.com/68745983/108010766-fb3d8000-7048-11eb-822b-1a035dc28c17.png)    
	* h(t-1)즉, 이전에 학습한 결과 값 + 현재 input을 기반으로 학습을 하여 다음에 나올 character를 예측하도록 한다.   
4. 이제 hidden layer를 통해 학습되어 나온 output값을 통해 다음에 나올 character를 찾아낸다.   
	* ![image](https://user-images.githubusercontent.com/68745983/108011012-86b71100-7049-11eb-980b-2acba232ae29.png)    
	* 각 timestamp 마다 다음에 나올 character를 예측한다.    
	* outputlayer를 통해 값을 예측한다.    
	* ![image](https://user-images.githubusercontent.com/68745983/108011098-b49c5580-7049-11eb-8a1f-412fabe28cb1.png)   
	* output vector는 기존에 정의된 사전의 크기와 동일하다.   
	* 결과 값에서 제일 높은 확률을 가진 character를 가져오기 위해 softmax를 통해 그 값을 가져온다.  
	* 이제 원하는 결과 값을 가지기 위해 계속해서 training을 해준다.   

> 처음 넣은 데이터값의 return 값을 그 다음 timestamp의 input값으로 활용한다면 무한정으로 학습이 가능하다.  
> 주식 값 예측...?
> 셰익스피어 글쓰기 [참고할 블로그](https://medium.com/towards-artificial-intelligence/ai-writes-shakespearean-plays-e0d5f30c16b2)   

### Backpropagation through time (BPTT)       


<p align="center"><img src="https://user-images.githubusercontent.com/68745983/108011985-96cff000-704b-11eb-9302-f892bf85a792.png" /></p>       


* 매 timestep마다 주어진 character에서 발생된 hidden state vaetor-> output layer를 통한 예측값과 label값을 비교하여 loss값을 구한다.  
	* Wxh : input layer에서 hidden layer로 값을 넘겨줄 때 가중치   
	* Whh : 이전 input들에 대한 연산값을 현재 input값과 연산될 때, 이전 값에 가해지는 가중치   
	* Why : hidden state에 결과 값을 output layer에 넘겨줄 때 가중치   
* BPTT는 이러한 Wxh, Whh, Why을 알맞게 튜닝하기 위해 연산한다.   
* input이 너무 길면 자원이 부족해질 수 있는 문제가 생긴다.   
* sequence를 나누어서 학습하자.    
	* ![image](https://user-images.githubusercontent.com/68745983/108012365-89673580-704c-11eb-99f8-98e882bd799f.png)


### RNN에는 좋기만 할까??   
* 문제점이 존재한다. **그 문제점에 대해 알아보자.**   
RNN을 간단히 그림으로 나타내면 아래와 같다.    

<p align="center"><img src ="https://user-images.githubusercontent.com/68745983/108014009-4e670100-7050-11eb-915a-a556af6482eb.png" /></p>     

그러면 이제 위의 그림을 식으로 나타내어 생각해보자.     
<p align="center"><img src="https://user-images.githubusercontent.com/68745983/108014211-bddcf080-7050-11eb-863a-d6ef288aeccc.png" /></p>    

위의 식을 확인해본다면, **Backpropagation**을 할때, 
* W의 절대값이 1이하이면 계속해서 곱한다면 기울기가 **0**에 가까워져 **<span style="color:orange">Gradient Vanshing</span>**이 야기될 수 있다.    
* W의 절대값이 1이하이면 계속해서 곱한다면 기울기가 **inf**에 가까워져 **<span style="color:orange">Gradient Exploding</span>**이 야기될 수 있다.
## 2. LSTM and GRU     
### Long Short Term Memory (LSTM)    
* **IDEA : transformation없이 직관적인 cell state 정보 전달**   
* Original RNN에서 **<span style="color:orange">Long Term Dependency</span>**를 해결한 Model이다.   
* Original RNN의 **<span style="color:orange">Gradient Vanshing</span>**과 **<span style="color:orange">Gradient Exploding</span>**을 해결해준다.   


<p align="center"><img src="https://user-images.githubusercontent.com/68745983/108015176-f41b6f80-7052-11eb-8fe6-d8abc61ceedd.png" /></p>     


* hidden state를 단기기억을 담당하는 소자로 생각할 수 있다.   
* ![image](https://user-images.githubusercontent.com/68745983/108020180-26cb6500-705f-11eb-814f-7deb013d669d.png)   
* 위의 수식과 같이 LSTM에서는 Ct-1이라는 값이 더 추가해서 연산된다.   
	* Ct-1 : Cell state vector   
* Cell state vector가 hidden state vector보다 완성된 정보를 가지고 있다.   
* hidden state vector는 Cell state vector를 한번더 가공해서 노출할 필요가 있는 정보만을 남긴 Vector이다.    

#### How Training?   
 
 
<p align="center"><img src="https://user-images.githubusercontent.com/68745983/108020425-b40eb980-705f-11eb-9017-b7c1468e5535.png" /></p>      


* Xt와 Ht-1을 입력으로 받아서 vector를 선형 변환한 후, output vector를 분할 해서 각각의 vector를 sigmod로 계산하는데, 마지막 값은 tanh로 연산을 한다. 각각의 연산된 vector를 아래와 같이 명명한다.   
	* i : input gate   
	* f: forget gate   
	* o : output gate   
	* g : gate gate   
* 해당 vector들은 cell state vector, hidden state vector를 계산하기까지 사용되는 **중간 결과물**로써 사용이 된다.   
* i, f, o는 sigmoid 함수를 통해 연산되기에 0~1의 가진다.   
* 즉, 원래 값의 일부를 가지도록 해주는 역할을 한다.    
* g의 값은 -1 ~ 1의 값을 가진다. 즉, 현재 timestep에서 유의미한 값을 가지도록 해준다.   

##### 1. 얼마나 많은 정보가 cell state로부터 흘러갈지 제어하기위해 gate를 사용한다.   

<p align="center"><img src="https://user-images.githubusercontent.com/68745983/108021060-1916df00-7061-11eb-90fd-b3d467f470c7.png" /></p>   
 
 
* 전 timestep에서 넘어온 Ct-1을 적절하게 변환해서 중간 결과물인 i, f, o, g를 만들어 낸다.   


##### 2. Forget gate?   

<p align="center"><img src="https://user-images.githubusercontent.com/68745983/108021268-83c81a80-7061-11eb-8e82-78375dde1d72.png" /></p>      


* 이전 timestep에서 넘어온 값을 얼마나 잊을지, 얼마나 기억할지 계산하는 gate이다.     

<p align="center"><img src="https://user-images.githubusercontent.com/68745983/108021441-ed482900-7061-11eb-95de-7ee06e83e29b.png" /></p>    

##### 3. Gate Gate?   
   
	 
<p align="center"><img src="https://user-images.githubusercontent.com/68745983/108021561-241e3f00-7062-11eb-9636-3e910e50fd62.png" /></p> 


* 이전 cell state vector를 f를 통해 적당한 비율로 정보를 잊게 만들어 왔을 때, 
* 해당 연산에서는 해당 state에서 들어온 input data를 적당한 비율로 기억을해서 해당 state에서의 cell state vector를 만들어 낸다.   
* ![image](https://user-images.githubusercontent.com/68745983/108022556-1cf83080-7064-11eb-8c51-6bf239721439.png)    
 

##### 4. Output Gate and Hidden State vector   


<p align="center"><img src="https://user-images.githubusercontent.com/68745983/108022750-82e4b800-7064-11eb-86b1-ee512b4e2c86.png" /></p>   


* Cell state vector가 가지던 값에서 적절한 비율로 그 값을 적게 만들어서 hidden state vector를 만든다.   
* Ct는 기억해야하는 모든 정보를 압축해서 가지고 있다.  
* 반면에 ht는 현재 timestep에서 직접적으로 필요한 정보만을 가진다.   
* ![image](https://user-images.githubusercontent.com/68745983/108023042-174f1a80-7065-11eb-82c9-e0f9eaed5363.png)    

### Gated Recurrent Unit (GRU)    
* LSTM을 경량화 해서 더 빠른 속도와 적은 메모리를 사용하는 Model이다.   
* LSTM의 cell state vector와 hidden state vector를 통합하여 hidden state vector만을 사용한다.   
* LSTM과 동작 원리가 매우 비슷하다.   
* ![image](https://user-images.githubusercontent.com/68745983/108024292-a3624180-7067-11eb-8678-2101a6b08daf.png)    


## 3. Plus Question   

* 1 BPTT 이외에 RNN/LSTM/GRU의 구조를 유지하면서 gradient vanishing/exploding 문제를 완화할 수 있는 방법이 있는지 찾아보자.   

* 2 RNN/LSTM/GRU 기반의 Language Model에서 초반 time step의 정보를 전달하기 어려운 점을 완화할 수 있는 방법을 찾아보자.    
























## 4. 이모저모   

1. 강의   
	* 오늘은 자연어 처리 model인 LSTM과 GRU에 대해 배웠다.   
	* RNN을 자연어 처리뿐만아니라 이미지 학습도 가능하다는 것을 들었는데
	* 오늘 배운 LSTM을 활용하여 이미지 분류를 해보아야겠다.
2. 피어세션
