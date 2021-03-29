---
title: "[BoostCamp] P-stag Image Classification day1"
layout: single
author_profile: true
read_time: true
comments: true
share: true
toc: true
related: true
toc_sticky: true
toc_label: content
categories:
- BoostCamp_AI_Tech
tags:
- Pstage_Image_Classification
---

# [BoostCamp] P-stage stage1 이미지 분류 day1  
---   

## 오늘의 목표
1. `Competition`의 목표를 세워보자.
2. `Competition`을 위한 환경설정을 해준다.

## 1. Competition의 목표??

* pytorch를 이용하여 image classification 프로젝트를 수행해보자.
* notebook 환경이 아닌 idle환경에서 프로젝트를 진행해보자.
* EDA를 직접해보면서 데이터에 대한 이해를 해보자.

## 2. Competition 환경설정 셋팅하기

### 서버 셋팅  

서버의 경우에는 boostcamp측에서 제공을 해주었다. 여기서 나는 주어진 두가지 GPU들 중(V100 또는 P40) 하나를 선택하여 서버를 배당 받으면 되었다.   
배당 받은 서버에는 competition에 필요한 데이터들이 준비되어있었다.   
나는 모델과 코드를 작성하여 해당 데이터를 train 시켜 나온 test값을 제출하기만 하면 된다.   
![image](https://user-images.githubusercontent.com/68745983/112866930-4e4d2d00-90f5-11eb-89b9-68b9a7f55a67.png)

### VScode 연동해서 코딩하기
※ 해당 설정은 window환경에서 진행된다.   

1. server를 할당받을 때 같이 다운로드된 key파일을 user\.ssh\ 디렉토리로 옮긴다.    
2. local에서 ssh를 사용하기 위해 설정 > 앱 및 기능 > 선택적 기능에서 `ssh client`를 설치한다.   
	* ![image](https://user-images.githubusercontent.com/68745983/112869596-4e026100-90f8-11eb-8bb0-75506e43bb56.png)    
3. 여기서 커맨드 창에 `ssh -i .ssh./key [user name]@[user address] -p [user port]` 명령을 입력하여 잘 실행된다면 여기까지 잘 따라온것이다.   
4. vscode의 extensions항목에서 remote ssh를 설치한다.  
	* ![image](https://user-images.githubusercontent.com/68745983/112868112-a6386380-90f6-11eb-86f4-a350537a7c86.png)    
5. 이제 `config`파일을 작성하여 vscode에서 ssh 접속을 해보자.    
	* ![image](https://user-images.githubusercontent.com/68745983/112871096-dd5c4400-90f9-11eb-9083-930b257298ef.png)
	* **Host** : 접속할 서버의 별명   
	* **HostName** : 접속할 서버의 주소   
	* **Port** : 접속할 서버의 접속할 ssh port    
	* **IdentityFile** : key file 주소   
6. 이제 vscode에서 서버의 ssh에 접속을 해보자.   
	* ![image](https://user-images.githubusercontent.com/68745983/112871631-670c1180-90fa-11eb-8bcc-fd7f5e063212.png)   
	* ![image](https://user-images.githubusercontent.com/68745983/112871913-b8b49c00-90fa-11eb-9e2a-6ffc2341e2de.png)   
7. 짠!!!!! 디렉토리까지 연결해주면 이제 vscode에서 서버단의 코드를 작성할 수 있다.   


## 3. TODO LIST   
1. EDA를 통해 데이터를 분석해본다.   
2. Dataset class를 생성한다.   
3. pytorch에서 제공하는 기본 모델들을 활용하여 학습시켜본다.
