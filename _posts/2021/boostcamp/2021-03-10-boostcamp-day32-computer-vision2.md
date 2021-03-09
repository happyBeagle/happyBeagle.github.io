---
title: "[BoostCamp] DAY32 Computer Vision#2"
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

# [BoostCamp] DAY32 Computer Vision#2
---   

## 1. Image Classification Ⅱ    
### 1.1 Problems with deeper layers    
#### Going deeper with convolutions   
* AlexNet과 GoogLeNet을 통해 더 깊은 네트워크가 더 좋은 성능을 낸다는 것을 알 수 있었다.   
	* 깊으면 더 복잡한 관계에 대해 학습이 가능하다   
	* 더 넓은 recptive field에 대해 학습이 가능하다.    
	* ![image](https://user-images.githubusercontent.com/68745983/110476574-76b0bf80-8125-11eb-9e27-d432956a0061.png)   


#### Hard to optimize    
* 그런데, **정말로 네트워크가 깊을 수록 학습이 더 잘될까?**   
	* **NOPE!!**   
	* Gradient Vanishing 혹은 exploding이 발생한다.   
	* ![image](https://user-images.githubusercontent.com/68745983/110476800-bf687880-8125-11eb-8340-0e045b3648f8.png)    
	* 계산 복잡도가 더 복잡해진다.   
	* model parmater가 너무 많아져서 **Overfitting**에 문제가 우려된다.--> Overfitting이 아니라 **Degradation problem**이 발생한다.   

> **Degradation Problem?**   
> Depth가 깊어질때, Gradient Vanishing 혹은 Exploding 문제에 의해 성능이 떨어지는 현상을 일컫는다.   


### 1.2 CNN architectures for image classification 2    
#### GoogLeNet   

* Inception module 제안
	* 하나의 layer에서 1x1 convolutions, 3x3 convolutions, 5x5 convolutions과 3x3 max pooing을 활용하여 **여러 측면으로 activation을 관측**한다.   
	* 수평확장으로 concatenate를  진행하여 모든 filter의 output을 합친다. (channel 단위로 합쳐진다.)    
	* ![image](https://user-images.githubusercontent.com/68745983/110477478-8da3e180-8126-11eb-968f-a7fe3f6bfd21.png)    
	* 그런데 여기서 하나하나 모든 convolution작업을 하려고한다면 계산 복잡도가 커질것으로 예상된다.   
	* **그렇다면 1x1 convolution을 bottleneck layer로 활용해보자**   
	* ![image](https://user-images.githubusercontent.com/68745983/110477825-fb500d80-8126-11eb-96ff-d3a166dfb320.png)    

> **1x1 convolution layer의 역할?**    
> ![image](https://user-images.githubusercontent.com/68745983/110479320-9c8b9380-8128-11eb-9530-1281ca9aa3bc.png)    
> 1. n\*h\*w의 크기의 input에서 특정 지점 여기서는 (-1, 0, 0)위치라고 하자. 해당 위치에 해당하는 값들을 vetorize한다.   
> 2. 그리고 같은 크기의 vector 즉, 1x1 convolution filter와 내적한다.   
> 3. (0, 0)의 위치에 결과값을 반환한다.   
> 즉, 1x1 conv는 채널을 압축할 수 있다.    


* GoogLeNet의 전반적인 architecture   
	* ![image](https://user-images.githubusercontent.com/68745983/110479942-45d28980-8129-11eb-8174-bcbcf20af72c.png)    
	* 초반은 vanila convolution network를 활용한다.   
	* 이후, **inception module**을 각 층마다 쌓아가며 학습한다.   
	* 여기서 우리가 주목해야할 부분이 존재한다.   
	* ![image](https://user-images.githubusercontent.com/68745983/110481031-7830b680-812a-11eb-8044-ba956310efd6.png)   
	* **Auxiliary Classifier**   
		* 네트워크가 깊게 쌓이면 Gradient Vanishing 혹은 Exploding이 발생한다.    
		* 이를 예방하기 위해 중간 결과 값을 따로 저장하여 해당 problem이 발생하는 것을 예방한다.  
		* 다만, 해당 과정은 Training과정에서만 수행한다. 즉, Testing 과정에서는 해당 과정을 삭제한다.    


#### ResNet    

* ![image](https://user-images.githubusercontent.com/68745983/110482782-5c2e1480-812c-11eb-81f4-05285ab88ef6.png)  
	* 깊이가 깊어질수록 error가 더 커진다는 것을 알 수 있다.   
		* overfitting 문제라고 하기에는 training set에서의 학습에서는 56층의 layer로 학습한 모델의 error가 더 적어야한다.  
		* 그런데 그렇지않음으로 overfitting문제로 생각하기에는 어려움이 존재한다.   
		* Network depth를 더 쌓는데에는 overfitting 문제가 아니라 **Optimization**문제라고 생각해보자.    
		* 앞선 gradient vanishing, exploding문제라고 생각한다.   
	* 앞선 googLeNet에서 깊은 네트워크를 만들었지만, 한계가 존재했다.   
	* 이를 넘어선 모델인 즉, 100개의 층을 넘겨 성능을 보인 **ResNet**에 대해 알아보자.   
* ![image](https://user-images.githubusercontent.com/68745983/110484031-a49a0200-812d-11eb-9ef1-270564c0245b.png)   
	* Plain layer로 학습해서 원하는 weight를 찾는데에는 어려움이 있는 것으로 보인다.   
	* 현재 주어진 identity외에 잔여부분F(X)을 학습하게 한다면 학습하는데 부담이 덜 나지 않을까 생각을 해보자.   
		* H(X) = F(X) + X로 표현을 할 수 있다.   
		* 이는 달리 생각해보면 F(X) = H(X) - X라고 표현이 가능하다.   
		* 이는 즉, H(X)가 아무리 복잡하더라도 이전의 값을 유지하려는 노력을 +X과정으로 인해 하지 않아도 된다.   
		* 또한 기존의 X와의 잔차 즉, F(X)만을 학습하면 되기에 기존의 plain layer학습보다 어려움이 덜할 것이다.   
	* 여기에서 이를 구현하기 위해서 우리는 shortcut conection에 대해 알아봐야한다.    
		* backpropagation을 할때, shortcut을 통해 흐를 수 있는 chance도 존재한다.   
		* X를 통해 갈때에는 gradient vanishing문제를 해결할 수 있었다.    
	* ![image](https://user-images.githubusercontent.com/68745983/110495466-e039c980-8137-11eb-8b5c-1c9724efd7d7.png)    
		* 2^n의 경우의 수로 gradient가 지날 수 있는 path가 생성된다.   
		* 결국, 다양한 경로를 통해 복잡한 mapping을 해내기 때문에 성능이 더 좋다는 분석이 존재한다.    
		* [관련 논문](https://arxiv.org/pdf/1605.06431.pdf)   
* 전체 구조 탐구   
	* ![image](https://user-images.githubusercontent.com/68745983/110496443-d1074b80-8138-11eb-9300-d7601da5948b.png)   
	* 처음 residual block전의 처리는 H(X) = F(X) + X의 연산을 하기위해 convolutional layer의 output의 shape과 맞춰주기 위해 사용된다.    


#### Beyond ResNet    

* **DenseNet**   
	* channel축으로 concatenation을 시행한다.   
		* 더하기 : 두가지 신호를 합친다. 
		* concatenation : 두가지 신호를 잇기때문에 메모리, 계산적으로는 불리하지만, 데이터는 보존된다.   
	* 바로 직전의 block의 입력을 받는 것뿐만아니라 훨씬 이전의 block의 입력을 받는다.   
	* 상위 레이어에서도 하위레이어의 특징을 참조할 수 있는 기회가 생긴다.   
* **SENet**   
	* depth를 높이거나 connection을 새로하는 방법이 아니라, 현재 주어진 activation이 더 명확해질 수 있도록 채널간의 관계를 리모델링한다.   
	* 채널간의 Attention을 할 수 있도록 한다.    
		* squeeze : global average pooling을 이용하여 각 채널의 공간 정보를 없애고 채널의 평균 정보를 포함하여 채널의 분포를 구한다.   
		* Excitation : FC레이어를 통해서 채널간의 관계를 알아본다.    
* **EfficientNet**   
	* network architecture를 설계할 때, 새로운 방법을 제시함   
	* 어떻게 효율적으로 학습을 할 수 있을까?    
* **Deformable convolution**    
	* irregular convolution layer가 제안이 되었다.   
	* 사람, 동물의 움직임을 확인할 때 상대적 위치가 바뀌는것에서 착안    
	* 2D offset과 standard CNN을 활용하여 구현    


## 2. Semantic Segmentation    
### 2.1 Semantic segmentation    
#### What is semantic segmentation?   
#### Where can semantic segmentation be applied to?    
### 2.2 Semantic Segmentaion architectures   
#### Fully Convolutional Networks (FCN)    
#### Hypercolumns for object segmentation   
#### U-Net   
#### DeepLab
