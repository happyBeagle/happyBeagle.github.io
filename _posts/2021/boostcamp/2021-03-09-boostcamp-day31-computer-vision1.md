---
title: "[BoostCamp] DAY31 Computer Vision#1"
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- BoostCamp_AI_Tech
tags:
- Computer_Vision
toc: true
toc_sticky: true
toc_label: contents
---

# [BoostCamp] DAY31 Computer Vision#1
---   

## 1. Image Classification Ⅰ    
### 1.1 Image Classification   
#### What is classification?   

* **Classifier**  
	* A mapping f(\.) that maps an image to a category level   
	* 영상 입력을 카테고리 레벨의 출력으로 변환시켜주는 과정을 분류기 즉, Classifier라고 한다.  

#### An ideal approach for image recognition   

* 어떻게 분류기를 구현할 수 있을 까?   
	* 가장 이상적인 분류모델은 무엇일까?   
	* 이 세상의 모든 데이터를 가지고 있다면 분류를 잘할 수 있지 않을까?   
		* **KNN**을 활용하여 search할 수 있지 않을까?   
	* 근데, 데이터가 많아지면 time complexity, memory complexity 즉 시스템 복잡도가 올라가서 현실적으로는 어려움 있다.   
	* 또한 데이터간의 유사도를 어떻게 정의를 할 수 있을까?    

> KNN? - K Nearest Neighbors   
> 가까운 데이터 k를 뽑아서 입력 데이터가 어디에 속하는지 분류하는 알고리즘이다.   



#### Convolutional Neural Networks   

* 방대한 데이터를 제한된 복잡도의 시스템에 압축해서 녹여놓자. --> Neura Network   

##### Before CNN   

* **Single Layer Neural Network**  
	* Fully-connected layer라고 불린다.   
	* ![image](https://user-images.githubusercontent.com/68745983/110335159-e613aa00-8066-11eb-8224-f07a4102c54f.png)    
	* 각각의 pixel들을 서로 다른 가중치를 주어 연산한 후, 분류를 해보자!   
	* 레이어가 한 층이라 단순하다. 
	* 평균값으로 이미지를 분류하기 때문에 평균 이미지 외에는 분류가 어렵다.   
	* 적용 시점, 즉 테스트 타임에서 문제가 있다.    
		* 이는 학습할때의 이미지를 변형(자르거나 줄이거나)한다면 원하는 값을 얻기 힘들다는 의미이다.    

##### Convolutional Neural Networks    

* **locally connected **  
	* 하나의 특징을 뽑기 위해 모든 픽셀을 고려하는 것이 아니라, 하나의 특징을 영상의 공간적 특성을 고려하여 국부적인 영역만 고려하는 것 
		* 파라미터 감소 효과  
	* 영상 여러 곳에서 특징 발현 가능성 존재    
		* sliding window처럼 순회하며 값을 가져오자   
	* Overfitting 문제 예방 가능 
	* backbone network로 많이 활용된다.    
	* ![image](https://user-images.githubusercontent.com/68745983/110338784-bebedc00-806a-11eb-958d-dde5199cd324.png)    


### 1.2 CNN architectures for image classification 1  
#### LeNet    

* 매우 단순한 CNN 구조이다.  
	* **Conv -> Pool -> Conv -> Pool -> FC -> FC**   
	* Conv filter는 5x5의 size, stride = 1의 크기와, 스트라드를 가진다.    
	* Pooling layer는 2x2크기의 max pooling filter로써 stride = 2이다.   
	* ![image](https://user-images.githubusercontent.com/68745983/110347094-9ab3c880-8073-11eb-8e64-0e46c000fc86.png)    

#### AlexNet   

* AlexNet은 LeNet과 유사한 것들이 많다. 하지만 어떤 차이점으로인해 더 좋은 성능을 가지게 되었는지 알아보자.   
	* model이 더 커졌다.   
		* hidden layer가 7개로 늘어났다.    
		* 605k개의 뉴런을 사용한다.   
		* 60000000개의 파라미터 연산을 한다.   
	* 학습에 사용한 데이터셋이 커졌다.
	* 활성 함수로 ReLU를 사용하고 정규화 기술로 Dropout을 사용하였다.   
* **Conv -> Pool -> LRN -> Conv -> Pool -> LRN -> Conv -> Conv -> Pool -> FC -> FC -> FC**    
	* ![image](https://user-images.githubusercontent.com/68745983/110350417-09deec00-8077-11eb-9e9f-a9c9811d9130.png)  
	* 당시의 컴퓨팅 파워를 보완하기 위해 두개의 GPU를 이용하여 연산하였다.
	* 요즘은 LRN(Local Response Normalization)을 잘 사용하지 않는다.   
		* Activation map에서 주로 명암을 좀 더 잘 구분하도록 사용을 했다.   
		* 하지만 그다지 성능이 보이지않아 사용하지 않는다.   
		* **대신 최근에는 Batch Normalization**을 사용한다.     
	* 11x11 conv filter을 사용하지 않는다.   
		* filter의 크기가 증가하면, 이미지의 input 사이즈 또한 증가한다.  
		* 큰 사이즈의 filter는 input이미지의 더 넓은 범위에 사용된다.   
		* 다만 요즘은 잘 사용하지 않는다.   

#### VGGNet

## 2. Annotation data efficient learning    
### 2.1 Data augmentation   
#### Learning representation of dataset  
#### Data augmentation   
#### Various data augmentation methods   
#### Modern augmentation techniques   
### 2.2 Leveraging pre-trained information   
#### Transfer learning   
#### Knowledge distillation   
### 2.3 Leveraging unlabered dataset for training   
#### Semi-supervised learning   
#### Self-training
