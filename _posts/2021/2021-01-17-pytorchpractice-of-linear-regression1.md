---
title: "[Pytorch]Practice of Linear Regression#1"
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Machine-Learning
tags:
- Machine-Learning_basic
- PyTorch
- LinearRegression
toc_sticky: true
toc: true
toc_label: contents
---

## Practice of Linear Regression #1(feat. PyTorch)   


### House Prices with Built Year
집이 지어진 년도에 따른 집의 가격을 예측해 보자.   
데이터는 [Kaggle](https://www.kaggle.com/c/house-prices-advanced-regression-techniques/overview)에서 가져 왔다.   
먼저 학습 데이터를 가져오자.   
**※ML 학습은 Colab에서 진행하였다.**   

#### 1.데이터 가져오기   
![image](https://user-images.githubusercontent.com/68745983/104689252-8de6b880-5745-11eb-9d6a-a7b37442eba0.png)
위 와 같이 코드를 입력한 후에 kaggle.json파일을 업로드 해준다.

>kaggle.json파일은 kaggle사이트에서 아래의 그림처럼 다운 받을 수 있다.   
>![image](https://user-images.githubusercontent.com/68745983/104689990-f1251a80-5746-11eb-8824-0cd1fd4121a1.png)   
> **Create New API Token**을 클릭하면 kaggle.json파일이 다운로드 된다.   

![image](https://user-images.githubusercontent.com/68745983/104690230-67c21800-5747-11eb-970d-8f2ba7aed60d.png)  
그 후, kaggle.json파일의 권한을 변경해준 다음,  
![image](https://user-images.githubusercontent.com/68745983/104690788-6c3b0080-5748-11eb-800a-5744f94c1812.png)   
위와 같이 데이터 파일을 다운로드 받으면 된다.   

> data를 다운 받기 위해서는 해당 competition에 등록하여야한다.
> ![image](https://user-images.githubusercontent.com/68745983/104690717-4c0b4180-5748-11eb-89db-da058db1e15a.png)   

##### 1) 데이터 분류   
이제 다운로드 받은 데이터를 training data, test data로 분류를 시켜줘야 한다.
>**[TIP] Why do this?**  
> training data만으로 학습을 시킨다면 과적합 문제가 발생할 가능성이 있다.
> > **과적합 문제(overfitting)**
> > ML 모델이 training data에 과하게 맞춰져서 실전에서 제대로 된 답을 도출 해내지 못할 때   
> > ![image](https://user-images.githubusercontent.com/68745983/104693197-968ebd00-574c-11eb-9d08-d066593cc779.png)  
> > 원래는 위와 같이 data가 분류되야 한다고 생각한다면,   
> > model이 위의 data set에 과하게 적용되어서 **Over Fitting**이 발생한다면,   
> > ![image](https://user-images.githubusercontent.com/68745983/104693403-eff6ec00-574c-11eb-9d55-6df5142b0b40.png)   
> > 위 와 같이 data set에 매우 적합한 model이 되어  
> > 다음에 들어올 data의 정확도를 확답할 수 없게 된다.   

![image](https://user-images.githubusercontent.com/68745983/104696489-b2489200-5751-11eb-8e3b-747eae97c916.png)   

* **pd.read_csv(r"./train.csv")**  
	pandas를 활용하여 csv파일을 읽어온다.   
* **train_data.SalePrice.values**   
	csv파일을 통해 가져온 data에서 label이 되는 SalePrice(집 가격) data를 가져온다.   
* **train_data.YearBuilt.values**   
	csv파일을 통해 가져온 data에서 feature이 되는 YearBuilt(집이 지어진 년도) data를 가져온다.   
* **tain_test_split(features, label, test_size = 0.2, random_state=42)**
	* feature : 학습에 필요한 특성 데이터를 입력한다.
	* label   : 학습의 label데이터를 입력한다.
		* feature와 label을 한데 묶어 data로 입력할 수 있다.
	* test_size : test data의 비율을 정해 준다.   
	* random_state : 랜덤으로 데이터를 분리하는데 seed를 정해준다.   
	* shuffle : False로 데이터를 순서대로 뽑을 수 있다. default = True   

* **torch.from_numpy()**   
	torch의 tensor형으로 데이터를 변형한다.   
    
##### 2) DataLoader
모든 data를 한꺼번에 학습시키기엔 무리가 있다.   
* *현재 예제의 데이터는 약 1500개 정도,*   
  *하지만 data가 수백만개를 넘어간다면 모든 데이터를 한꺼번에 처리하기는 어렵다.*   

* **Batch**
전체 데이터를 나눠 일부를 묶은 데이터 단위   

* **Epoch**   
한번 **모든**트레이닝 데이터에 대해 한 번 학습함  
* **Iterations**   
epoch를 나누어서 실행하는 횟수   

>**Examples**
>총 데이터가 1000개, batch_size = 100이라면,   
>1 iteration => 100개의 데이터를 학습   
>1 epoch     =>  1000 / batch_size = 10 iteration   

![image](https://user-images.githubusercontent.com/68745983/104703829-2cc9df80-575b-11eb-8255-18b2af171565.png)   
* **torch.utils.data.TensorDataSet(features, label)**   
	이전에 분류해 놓은 feature과 label을 하나의 dataset으로 묶어 준다.   
* **DataLoader(data, batch_size, shuffle=False)**   
	csv로 불러온 data를 원활히 학습할 수 있도록 batch로 나눠서 학습에 적용 할 수 있도록한다.   
![image](https://user-images.githubusercontent.com/68745983/104833352-5742a680-58db-11eb-8edc-d9f8bfa4ac19.png)   

#### 2.학습하기   
![image](https://user-images.githubusercontent.com/68745983/104838242-017ef600-58fd-11eb-81f4-24779cfa8419.png)   
* **torch.zeros(1, requires_grad=True)**   
	초기 W, b값을 설정해 주기 위해 사용하였다.   
    *requires_grad*
    * 기본값은 FALSE이다.
    * autograd가 반환된 값을 해당 텐서에 적용해야 한다면,   
      **TRUE**로 설정한다.   
 
* **optim.SGD([W, b], lr=0.000001)**  
	최적화를 위해 Gradient Descent의 한 종류인 SGD를 사용하였다.
    * **optimizer.zero_grad()**   
    	기울기를 초기화 하기 위해 사용하였다.    
    * **cost.backward()**   
    	가중치 W와 편향 b에 대한 기울기를 계산한다.   
    * **optimizer.step()**   
    	 W와 b에서 구해진 변수들의 기울기에 학습률을 곱하여 빼줌으로서 업데이트합니다.   
     
#### 3.결과 보기   
![image](https://user-images.githubusercontent.com/68745983/104838287-5fabd900-58fd-11eb-9551-ce6d0f3007dd.png)   
10epoch마다 평균 cost를 계산해서 결과 값을 보았다. 아주 근소하게 cost값이 줄어드는 것을 확인할 수 있었다.   
더 빠르게 학습하기 위해서 learning rate를 크게 줘보았다.   
**learning rate가 0.000001일때**   
![image](https://user-images.githubusercontent.com/68745983/104838416-2889f780-58fe-11eb-9a4b-27a5f0028959.png)
위의 training 과정을 보면 cost값이 **NAN**으로 표시가 된것을 볼 수 있다.   
이 경우, learning rate이 너무 커서 **Over shooting**의 가능성을 생각해볼 수 있다.   


해당 데이터 셋의 문제에서는 집이 지어진 년도뿐만 아니라 여러 요소들을 고려하여 집의 가격을 예측하여야한다.   
즉, 우리는 다음 글에서 여러 feature를 이용하여 집 가격을 고려하는 문제를 해결해 보자.







###  Reference   
[03 선형회귀_선형 회귀 #1](https://wikidocs.net/53560)   
[cost 값이 NAN??_stack overflow](https://stackoverflow.com/questions/61989369/cost-becoming-nan-after-certain-iterations)   
[data set_house prices](https://www.kaggle.com/c/house-prices-advanced-regression-techniques)
