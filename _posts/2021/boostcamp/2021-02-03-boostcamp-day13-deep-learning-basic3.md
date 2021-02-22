---
title: "[BoostCamp] DAY13 Deep Learning Basic#3"
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

# [BoostCamp] DAY13 Deep Learning Basic#3
---   

## 1. Convolutional Neural Networks   
### 1) Convolution   
한국어로는 **<span style="color:orange">합성곱</span>**이라고 한다. Convolution을 식으로 표현하면 아래와 같다.   
1. **Continuous Convolution**   
![image](https://user-images.githubusercontent.com/68745983/106740204-6d7f8f00-665d-11eb-9d5f-427b0c531509.png)   
2. **Discrete Convolution**   
![image](https://user-images.githubusercontent.com/68745983/106740614-fdbdd400-665d-11eb-990b-f086bb8cb3d3.png)   
3. **2D image Convolution**   
![image](https://user-images.githubusercontent.com/68745983/106740946-686f0f80-665e-11eb-871e-4dcb49ef977f.png)    

이제 위의 식들 중 2D를 그림으로 표현하여 Convolution을 이해해보자.    
![image](https://user-images.githubusercontent.com/68745983/106742986-1f6c8a80-6661-11eb-9d89-53e712e68efd.png)   
Input과 kernel을 합성곱을 진행하면 아래의 식으로 표현이 가능하다.   
![image](https://user-images.githubusercontent.com/68745983/106743565-ebde3000-6661-11eb-983b-95ce4de2989b.png)

**어디에 활용될 수 있을까?**   
2D이미지를 예시로 든다면 Convolution을 이용하여 이미지를 Blur처리하거나 외곽을 구하는 등 다양하게 활용이 가능하다.    

### 2) RGB Image Convolution   
RGB 이미지는 Red, Green, Blue를 의미하는 각 2D matrix로 이루어져있다. 즉, 3\*N\*N tensor의 모양을 가진다.   
그리고 이를 Convolution하는 것을 그림으로 나타내보면 아래와 같다.   
![image](https://user-images.githubusercontent.com/68745983/106745115-01ecf000-6664-11eb-98a8-da1dad9dceb0.png)    
자, 그렇다면 1\*N\*N shape뿐만 아니라 k\*N\*N의 shape를 가지고 싶다면 어떻게 해야할까?     
![image](https://user-images.githubusercontent.com/68745983/106746051-5349af00-6665-11eb-957b-73d58b7a0263.png)

### 3) Stack of Convolutions   
Convolution Layer를 어떻게 쌓을 수 있을까?    
![image](https://user-images.githubusercontent.com/68745983/106750883-c9511480-666b-11eb-83b6-0ed509fe2849.png)   
n개 쌓인 filter로 convolution연산을 해주면 n두깨의 2D매트릭스가 생성된다.   

### 4) Convolution Neural Networks   
convolution Neural Networks는 convolution layer, pooling layer 그리고 fully connected layer등으로 이루어져 있다.   
* **Convolution and pooling layer**: 특징 추출   
* **Fully connected layer**: 결정 하기(예. 분류기)   
![image](https://user-images.githubusercontent.com/68745983/106751728-f2be7000-666c-11eb-9dcb-6902d369769b.png)   
> 출처 : https://www.kdnuggets.com/2016/11/intuitive-explanation-convolutional-neural-networks.html/3    

### 5) Stride & Padding   
#### Stride   
입력된 데이터를 필터에 적용할 때, 이동간격을 조절하는 것을 **Stride**라고 한다.   
![image](https://user-images.githubusercontent.com/68745983/106752799-34034f80-666e-11eb-80c5-8375f7b576b2.png)   
#### Padding   
데이터가 filter되기전 입력값의 둘레를 0또는 다른 값으로 채우는 것을 **Padding**이라고 한다.   
![image](https://user-images.githubusercontent.com/68745983/106753445-05d23f80-666f-11eb-8ebd-37d9708af140.png)   

**Padding을 사용하는 이유는 무엇 일까?**     
* 정보의 손실을 최소화하기 위해 padding을 사용한다.   

### 6) Convolution Arithmetic   
**Parameter는 어떻게 계산할 수 있을 까?**    
![image](https://user-images.githubusercontent.com/68745983/106755304-52b71580-6671-11eb-8128-ef00f0b0fd42.png)    
위의 예를 기준으로 파라미터를 계산해보자. 
* **parameter** : 3 \* 3 \* 128 \* 64 = 73,728   

## 2. Modern CNN   
### 1) AlexNet   
**AlexNet**은 ImageNet Large-Scale Visual Recognition Challenge 즉, **ILSVRC**에서 2012년에 우승한 모델이다.   
![image](https://user-images.githubusercontent.com/68745983/106756891-14baf100-6673-11eb-8c05-d02c867390e6.png)   
> 출처 : [AlextNet 관련 논문](https://papers.nips.cc/paper/2012/file/c399862d3b9d6b76c8436e924a68c45b-Paper.pdf)    

* **Key Ideas**   
	* ReLU activation   
		* 역전파 연산에서 나타나는 **vanishing gradient**문제를 해결해준다.   
		* ![image](https://user-images.githubusercontent.com/68745983/106764542-391acb80-667b-11eb-8edb-16d5b1896831.png)
 
	* GPI implementation (2 GPUs)   
	* Local response normalization, Overlapping pooling   
		* RelU함수에 의해 큰 값이 Conv나 Pooling연산으로 인해 주변 픽셀에 영향을 미치는 것을 억제하기 위해 사용한다.   
	* Data augmentation   
	* Dropout   
		* TODO Dropout에대해 정리하기   

### 2) VGGNet   
**ILSRC**에서 좋은 성능으로 평가 받은 모델이다.   
![image](https://user-images.githubusercontent.com/68745983/106766310-1be6fc80-667d-11eb-9627-d6e48801288a.png)   
* 3x3 convolution filter를 이용하여 깊이를 늘렸다.(stride = 1)   
* fully connected layer를 위해 1x1 convolution을 이용하였다.   
* dropout (p=0.5)   
* VGG16, VGG19   

**그런데 왜 3x3 conv를 사용할 까요?**  
* 5\*5conv를 한번 사용할때와 3\*3conv를 두번 사용하여 연산할때를 비교해보자.   
* ![image](https://user-images.githubusercontent.com/68745983/106768384-37530700-667f-11eb-8a54-383fbfa75505.png)    
* 5\*5 filter를 사용하는 것보다 3\*3 filter를 두번 사용하여 연산하는 것이 더 적은 parameter를 소모한다.   

### 3) GoogleNet   
**2014 ILSRC**에서 좋은 성능으로 우승한 모델이다.   
* Inception blocks   
	* ![image](https://user-images.githubusercontent.com/68745983/106770927-ca8d3c00-6681-11eb-8031-4bb1dd4d79fa.png)   
	* parameter의 수를 줄일 수 있다는 장점이 존재한다.  
	* 어떻게 parameter값을 줄일 수 있나요?   
		* 1x1 conv는 채널의 차원을 줄여줄 수 있다.  


### 4) ResNet   
**2015 ILSRC**에서 우승한 모델이다.  
* 학습을 하기 위해 더 깊은 neural network를 구성하는 것은 어렵다.   
	* Overfitting이 종종 원인이 된다.   
	* ![image](https://user-images.githubusercontent.com/68745983/106771840-c31a6280-6682-11eb-9965-518e512c0ce4.png)   
	* > 출처: 2015년 ResNet 논문   
* skip connection : f\`(x) = x + f(x)  
	![image](https://user-images.githubusercontent.com/68745983/106772132-0d9bdf00-6683-11eb-9a75-3e679412ded3.png)
* 조금 더 발전된 ResNet은 f\`(x) = conv(x) + f(x)의 목적식을 가지고 있다.   
* Batch normalization 뒤에 conv연산을 한다.   
* Bottleneck 구조를 사용하여 parameter의 수를 줄인다.   
	* ![image](https://user-images.githubusercontent.com/68745983/106772888-cc57ff00-6683-11eb-91e6-d9f20f0c0b69.png)   



### 5) DensNet   
* DenseNet은 ResNet의 구조에서 addition 대신, concatenation을 사용한다.   
	* ![image](https://user-images.githubusercontent.com/68745983/106773112-12ad5e00-6684-11eb-86a8-516820f31d51.png)   
	* x → [x, f1(x), f2(x, f1(x)).....]   
* Dense Block    
	* 각각의 layer는 모든 이전의 모든 레이어의 특징을 합친다.   
	* 채널의 수가 기하학적으로 증가한다.   
* Transition Block   
	* Batch Norm -> 1x1 Conv -> 2x2 AvgPooling  
	* 차원을 줄인다.   

## 3. Computer Vision Applications   
### 1) Sementic Segmentation   
각각의 물체를 구분하기 위해 사용한다. 예를 들어 자율주행 프로그램에서 차와 도로를 구분하기 위해 사용한다.  
#### Fully Convoltional Network   
![image](https://user-images.githubusercontent.com/68745983/106775318-5acd8000-6686-11eb-9ba4-6ead5dc57d7d.png)  
기존의 CNN을 보면 flat, dense등을 통해 결과값을 얻는다. **Fully Convolutional Network**는 convolutionalization을 통해 결과 값을 얻을 수 있다. 그렇다면 이를 통해 얻을 수 있는 이점은 무엇이 있을까?   
* 아래의 FC layer가 가지는 한계점을 해결해줄 수 있다.   
	* 이미지 위치 정보가 사라진다.   
	* 입력이미지의 크기가 고정된다.   
	* [참고 글](https://medium.com/@msmapark2/fcn-%EB%85%BC%EB%AC%B8-%EB%A6%AC%EB%B7%B0-fully-convolutional-networks-for-semantic-segmentation-81f016d76204)   

#### Deconvolution    
* Feature map의 크기를 증가시킨다.  
	* 동작 방법?   
		* 각각의 픽셀 주위에 zero padding을 추가한다.  
		* padding된 map에 convolution연산을 해준다.   


### 2) Detection   
#### R-CNN   
Input 이미지에 대해 후보 영역을 여러개 생성하여 CNN을 통해 특징을 추출해내는 모델이다.   
![image](https://user-images.githubusercontent.com/68745983/106777984-d6c8c780-6688-11eb-9be4-1a34f1576c58.png)   

#### SPPNet   
* R-CNN에서, crop/wrap의 수는 주로 2000이상에 달한다. 즉, CNN이 2000번 이상 실행되어야 한다는 것이다.    
* 그러나, SPPNet은 CNN을 한번만 실행한다.   
* ![image](https://user-images.githubusercontent.com/68745983/106778478-5f476800-6689-11eb-8ac8-9f3b51350fa1.png)   

#### Fast R-CNN   
* R-CNN보다 빠르다고 개발된 Fast R-CNN이다.    
* ![image](https://user-images.githubusercontent.com/68745983/106778823-b77e6a00-6689-11eb-9ad3-0610686d57ff.png)

#### Faster R-CNN   
* Fast R-CNN보다 더 빠르다고 개발된 모델이다.    
* Region Proposal Network + Fast R-CNN    


##### Region Proposal Network?    
![image](https://user-images.githubusercontent.com/68745983/106779313-370c3900-668a-11eb-97ac-2267fd21b3f2.png)
> ※이에 대해서는 다시 공부를 해야할 것같다.    

#### YOLO   
* YOLO는 정말 빠른 물체 detection 알고리즘이다.
* YOLO는 Image에서 box와 class를 동시에 예측한다.   
	* 주어진 이미지에서 YOLO는 SxS 크기로 이미지로 나눈다.
	* 각각의 cell은 B bounding box를 예즉한다.(여기서 B는 크기이다.)
	* 각각의 cell은 C개의 class의 확률을 예측한다.   
	* 이제 SxSx(B\*5+C)크기의 텐서를 가지게 된다.   



## 4. TODO   
1. 위에서 아직 학습하지 못한 부분에 대해서 복습하며 학습하자.  
2. 아직까지 읽지 못한 논문들이 많다. 읽고 공부하자.   
3. 오늘 학습중 나온 실습 부분을 실습하자.   
4. 코딩 공부를 게을리 하지 말자.   



## 5. 이모저모   
1. 강의   
* 오늘 배운 내용들은 정말 많았던 것같다. 이를 복습하기 위해 좀 더 많은 시간을 들여야할 것같다.   

2. 피어세션   
* 매번 피어세션을 할때마다 조원분들께 많은 것을 배워 가는 것 같다. 항상 감사하다.   
* 오늘 나온 조별과제에 대해 이야기를 나누었는데, 함께 학습하는 것에 기대가 된다.
