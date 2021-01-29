---
title: "[BoostCamp] DAY10 AI Math#5"
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- BoostCamp_AI_Tech
tags:
- Pandas
- BoostCamp_AI_Tech
toc: true
toc_sticky: true
toc_label: contents
---

# [BoostCamp] DAY10 AI Math#5
---   

## 1. Pandas 활용하기_Visualization    
### matplotlib   
* 파이썬의 대표적인 시각화 도구이다.   
* 다양한 graph를 지원하며 pandas와 연동된다.   
* `pyplot`객체를 사용하여 데이터를 표시한다.   
* `pyplot`객체에 그래프를 쌓은 다음 flush한다.   
* ~~가장 큰 단점은 argument를 kwargs로 받아 고정된 argument가 없어 alt+tab으로 확인이 어렵다.~~    

이제 matplotlib를 이용하여 여러 그래프를 그려보자.   
1. 가장 기본적인 그래프를 그려보자.  
```python    
y = x**2
```    
	![image](https://user-images.githubusercontent.com/68745983/106309254-339d3a00-62a5-11eb-9b80-b86968d51bec.png)   

2. 두개의 그래프를 하나의 좌표평면에 그려보자.
	* graph는 원래 figure객체에 생성된다.  
	* pyplot 객체사용시, 기본 figure에 그래프가 그려진다.    
	![image](https://user-images.githubusercontent.com/68745983/106309795-fa18fe80-62a5-11eb-9a66-f0c7fab0a125.png)    

3. 서로 다른 좌표평면에 그래프를 그려보자.   
![image](https://user-images.githubusercontent.com/68745983/106310354-c68aa400-62a6-11eb-8c4d-23eacb715249.png)   

	* ※ 참고 해두자.  
	* ![image](https://user-images.githubusercontent.com/68745983/106310394-d6a28380-62a6-11eb-8deb-32d805e283b5.png)    
	* 해당 예제의 그림에서는 2*3크기의 subplot가 총 6개 띄워져있다.   

4. color속성을 이용해 그래프에 색을 입히자.    
	```python   
	plt.plot(x_1, y_1, color="#eeefff")
	plt.plot(x_1, y_1, color="red")
	```   
5. 그래프의 선을 점선 등 다양한 모양으로 변경시키자.   
	```python   
	plt.plot(x_1, y_1, c='b', linestyle="dashed")
	plt.plot(x_1, y_1, c='g', ls="dotted")
	
	plt.title("test")#pyplot에 제목을 부여한다. subplot별 제목부여도 가능하다.  
	plt.title("$y = \\frac{ax + b}{test}$") #latex타입의 표현도 가능하다

	plt.legend(shadow=True, fancybox=true, loc="lower right") #범례를 표시해준다.   
	plt.grid(True, lw=0.4, ls="--", c=".90")#graph보조선을 긋는 grid와 xy축 범위 한계를 지정해준다.
	plt.xlim(-100, 200)
	plt.ylim(-200, 200) 
	```   
6. **scatter** 함수를 이용해보자.    
![image](https://user-images.githubusercontent.com/68745983/106311887-313cdf00-62a9-11eb-90a4-6eb2d744db87.png)   
[scatter marker 종류들](https://matplotlib.org/3.1.1/api/markers_api.html)   

7. 히스토그램을 그려보자.   
![image](https://user-images.githubusercontent.com/68745983/106312164-985a9380-62a9-11eb-8849-b38c6f4872c2.png)   

이외에도 bar, boxplot등 다양한 종류의 그래프를 그릴 수 있다.   

### seaborn   
* statistical data visualization   
* matplotlib를 더 쉽게 사용할 수 있도록 제작되었다.   
* 복잡한 그래프를 간단하게 만들 수 있는 wrapper이다.   
* matplotlib와 같은 기본적인 plot이다.   
* lineplot, scatterplot, countplot 등....   

**[PLUS] TIP**  
![image](https://user-images.githubusercontent.com/68745983/106312538-29316f00-62aa-11eb-937c-09553c92757b.png)    
![image](https://user-images.githubusercontent.com/68745983/106312612-49612e00-62aa-11eb-8004-f050ed24ed27.png)   


## 2. 통계학 맛보기
### 1) 모수 추정  
#### 모수의 정의    
**<span style="color:orange">통계적 모델링은 적절한 가정 위에서 확률 분포를 추정</span>**하는 것이 목표이며, 기계학습과 통계학이 공통적으로 추구하는 목표이다.   
 * 유한한 개수의 데이터만 관찰해서 모집단의 분포를 정확하게 알아낸다는 것을 불가능하다.
 * 따라서 **<span style="color:orange">근사적으로 확률분포를 추정</span>**할 수 밖에 없다.   

> **※ 알아두자**   
> * **<span style="color:green">모수적 방법론</span>** : 데이터가 특정 확률 분포를 따른다고 선험적으로 가정한 후, 그 분포를 결정하는 모수를 추정하는 방법   
> * **<span style="color:green">비모수 방법론</span>** : 특정 확률 분포를 가정하지 않고 데이터를 따라 모델의 구조 및 모수의 개수가 유연하게 바뀌는 방법론  

> 결국 **<span style="color:orange">확률 분포의 가정 유무</span>**에 따라 방법론의 type이 나뉜다.    


#### 모수를 추정해보자.     
모수를 추정가기 위해서는 확률 분포를 따른다고 가정을 해야한다. 그렇다면 어떤 확률 분포를 가정해서 모수를 추정해야할까?  

1. 우선 히스토그램을 통해 모양을 관찰한다.   
	* 데이터가 2개의 값(0 또는 1)만 가지는 경우 : **베르누이 분포**   
	* 데이터가 n개의 이산적인 값을 가지는 경우 : **카테고리 분포**    
	* 데이터가 [0, 1] 사이에서 값을 가지는 경우 : 베타 분포   
	* 데이터가 0 이상의 값을 가지는 경우 : 감마분포, 로그정규분포 등    
	* 데이터가 실수 전체에서 값을 가지는 경우 : **정규 분포**, 라플라스 분포 등  

<span style="color:pink">
※ 단, 기계적으로 확률 분포를 가정해서는 안 되며, **데이터를 생성하는 원리를 먼저 고려하여야한다.**    
※ 각 분포마다 검정하는 방법이 존재하므로 모수 추정후에는 검정이 반드시 있어야한다.   
</span>    

##### - 정규분포의 모수를 구해보자.  
정규분포의 모수는 평균μ와 분산 σ²으로 이를 추정하는 통계량은 아래와 같다.   
![image](https://user-images.githubusercontent.com/68745983/106275013-890f2200-6278-11eb-93db-13dbcffab78c.png)   

> 표본분산을 구할때 , N이아니라 N - 1로 나누는 것은 불편 추정량을 구하기 위해서이다.   
> * **불편 추정량?**   
> 추정량의 기대값이 모수와 같아진다면, 이 추정량을 `불편 추정량`이라고 한다.   
> --> 편향되지 않았다.라는 의미를 가지고 있다.
> 그래서 표본 분산을 계산할 때, N이 아닌 N-1으로 나누어 표본분산을 불편 추정량으로 만들어 준다.
> ~이에 관해서는 다음에 좀 더 자세히 다뤄보도록 하자.~  

* 결국 추정된 데이터들도 모수의 일부분이므로 기댓값을 구할 수 있다.    
	* 즉 표본 평균의 기댓값이 모수의 평균이고, 표본 평균의 분산의 기댓값이 모수의 분산이다.   
* 통계량의 확률 분포를 **<span style="color:orange">표집분포</span>**라 부르며, 특히 표본 평균의 표집분포는 N이 커질수록 정규분포 N(μ, σ²/N)을 따른다.

> **※ 모집단 분포 VS 표본 분포 VS 표집 분포**   
> * **모집단 분포** : 연구대상이 되는 전체 속성을 나타내는 분포   
> * **표본 분포** : 모집단의 속성을 알기 위해 모집단을 대표할 수 있게 추출된 대상군의 분포   
> * **표집 분포** : 가상적 분포(어떤 가정을 전제로 하여 이론적으로 그려질 수 있음) -> 이론적 분포   
> [참고 블로그](https://m.blog.naver.com/PostView.nhn?blogId=bboomm22&logNo=220768020794&proxyReferer=https:%2F%2Fwww.google.com%2F)  


##### - 최대가능도 추정법     
* 표본 평균이나 표본 분산은 중요한 통계량이지만 확률 분포마다 사용하는 모수가 다르므로 적절한 통계량이 달라지게 된다.   
* 이론적으로 가장 가능성이 높은 모수를 추정하는 방법 중 하나는 **<span style="color:orange">최대 가능도 추정법(MLE)</span>**이다.    
![image](https://user-images.githubusercontent.com/68745983/106278371-f70a1800-627d-11eb-8a2f-5807039c9b45.png)
   

>  ※ 가능도란?    
>  가능도 함수는 모수θ를 다르는 분포가 X를 관찰할 가능성을 뜩하지만 확률로 해석하면 안된다.   
>  **그렇다면 가능도란 무엇일까?**   
>  * **확률** : 주어진 확률 분포가 있을 때, 관측값 혹은 관측 구간이 분포 안에서 얼마의 확률로 존재하는 가를 나타내는 값이다.   
>  	* 확률 분포를 고정하고 그 때의 관측 X에 대한 확률을 구한다.   
>  	* 확률 = P(관측 값 X \| 확률 분포)   
>  * **가능도** : 어떤 값이 관측되었을 때, 이것이 어떤 확률 분포에서 왔을 지에 대한 확률이다. -->확률의 확률?  
>  	* 가능도는 = L(확률 분포 \| 관측값 X)  
>  	[참고 블로그](https://jjangjjong.tistory.com/41)  

* 데이터 집합 X가 **독립적으로 추출되었을 경우 <span style="color:orange">로그 가능도</span>를 최적화** 한다.   
![image](https://user-images.githubusercontent.com/68745983/106278265-c924d380-627d-11eb-9781-161ecf216b80.png)     


###### 로그가능도를 왜 활용할까?    
* 로그가능도를 최적화하는 모수는 가능도를 최적화하는 MLE가 된다.    
* 데이터의 숫자가 적으면 상관없지만 만약, **데이터의 숫자가 아주 방대하다면 컴퓨터의 정확도로는 <span style="color:red">가능도를 계산하는 것은 불가능</span>**하다.   
* 데이터가 독립일 경우, 로그를 사용하면 가능도의 곱셈을 **로그가능도의 <span style="color:blue">덧셈</span>으로 바꿀 수 있기 때문에 z컴퓨터로 <span style="color:blue">연산이 가능</span>**해진다.   
* 경사하강법으로 가능도를 최적화할 때 미분 연산을 사용하게 되는데, 로그 가능도를 사용하면 **연산량을 줄여준다.**   
	* **<span style="color:orange">O(n²) --> O(n)</span>**   
* 대게의 손실 함수의 경우 경사하강법을 사용하므로 **음의 로그가능도를 최적화**하게 된다.   

###### * 정규 분포    
정규분포를 따르는 확률 변수 X로부터 독립적인 표본{X₁, X₂, .....}을 얻었을때 MLE을 이용해서 모수를 추정해보자.   
![image](https://user-images.githubusercontent.com/68745983/106289744-fe84ed80-628c-11eb-85f6-6c76a35e0378.png)   
위와 같이 로그가능도를 사용하여 연산을 할 수 있다.   
이제 미분을 통해 가능도를 최대화 할 수 있도록 해보자.   
![image](https://user-images.githubusercontent.com/68745983/106291092-8ae3e000-628e-11eb-9f52-c9d3e1c683d4.png)   
※단, MLE는 불편추정량을 보장하진 않는다.  

[참고 글](https://towardsdatascience.com/maximum-likelihood-estimation-explained-normal-distribution-6207b322e47f)

###### * 카테고리 분포   
![image](https://user-images.githubusercontent.com/68745983/106298603-6ccead80-6297-11eb-83f5-46c21e71c71d.png)  
카테고리 분포는 위와 같이 표현된다. 더불어 카테고리 분포의 모수는 하나의 제약식이 존재한다.    
![image](https://user-images.githubusercontent.com/68745983/106298805-b8815700-6297-11eb-9c8f-52244d3e531c.png)  
그렇다면 이제 위의 식을 정리하여 라그랑주 승수법을 활용하여 하나의 식으로 만들어 보자.    
![image](https://user-images.githubusercontent.com/68745983/106301240-d43a2c80-629a-11eb-971f-c00437ff1bea.png)   
이제, 각각을 미분하여 모수를 추정할 수 있다.   
![image](https://user-images.githubusercontent.com/68745983/106301466-195e5e80-629b-11eb-978c-0383a2c37f83.png)   

> ※ 라그랑주 승수법이란?    
> def) 어떠한 문제의 최적점을 찾는 것이 아니라, 최적점이 되기 위한 조건을 찾는 방법 즉, 최적해의 필요조건을 찾기위한 방법이다.    
> [참고 블로그]((https://untitledtblog.tistory.com/96)


###### * 딥러닝에서의 최대가능도 추정법    
* 최대가능도 추정법을 이용해서 기계학습 모델을 학습할 수 있다.   
* 딥러닝 모델의 가중치를 θ = (W¹, W²,....)라 표기 했을 때 분류문제에서 소프트맥스 벡터는 카테고리 분포의 모수를 모델링한다.   
* 원핫벡터로 표현한 정답레이블 y =(y1, ...., yk)을 관찰데이터로 이용해 확률 분포인 소프트맥스 벡터의 로그가능도를 최적화할수 있다.   
![image](https://user-images.githubusercontent.com/68745983/106301957-ae615780-629b-11eb-933f-68c19452d458.png)    

### 2) 확률 분포의 거리  
* 기계학습에서 사용되는 손실함수들은 모델이 학습하는 확률분포와 데이터에서 관찰되는 확률 분포의 거리를 통해 유도한다.    
* 데이터공간에 두개의 확률 분포 P(X), Q(X)가 있을 경우 **두 확률 분포 사이의 거리**를 계산할때 아래와 같은 함수를 활용한다.   


#### 총 변동 거리    
#### 쿨백-라이블러 발산    
![image](https://user-images.githubusercontent.com/68745983/106302221-0730f000-629c-11eb-9b79-dd9523e96558.png)   
다만, 쿨백-라이블러 발산의 경우, P를 기준으로 재는 값과 Q를 기준으로 재는 값의 결과가 달라 거리 측정을 한다라고 하기에는 다소 무리가 있는 듯하다.   
#### 바슈타인 거리   








## 3. 그외 이모저모   
1. 강의  
* 오늘은 시각화와 통계학에 대해 배웠다.   
* 시각화는 내가 구현한 모델의 loss값을 보거나 데이터를 분석하는데 요긴하게 쓰일 것같아 좋았다.   
* 통계학은 아직까지 익숙치 않은 느낌이 다소 있다. 그래서 복습을 통해 좀더 잘 활용할 수 있도록 해야겠다.    

2. 피어 세션  
* 오늘의 피어세션에서는 수업의 리뷰와 조원분의 통계학 보강 수업을 들었다.  
* 어려운 부분이었는데 잘 설명해주셔서 이해가 더 잘 된것 같다.   

3. 나중에라도 공부할 내용
* [Pandas VS SQL speeed](https://blog.thedataincubator.com/2018/05/sqlite-vs-pandas-performance-benchmarks/)    
* [Pandas VS SQL pros and cons](https://www.quora.com/Is-Pandas-library-in-Python-a-good-alternative-to-SQL-What-about-the-pros-and-cons-of-each)   
* [라그랑주 승수법](https://untitledtblog.tistory.com/96)
* [Likelihood VS Probability](https://www.youtube.com/watch?v=pYxNSUDSFH4)
