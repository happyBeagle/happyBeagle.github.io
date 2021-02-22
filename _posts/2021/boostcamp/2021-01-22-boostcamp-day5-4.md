---
title: "[BoostCamp] DAY5 파이썬 기초 문법#4"
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- BoostCamp_AI_Tech
tags:
- Python
- BoostCamp_AI_Tech
toc: true
toc_sticky: true
toc_label: contents
---

# DAY5 파이썬 기초 문법#4
---   
## 1. Exception    
1. 예상이 가능한 예외   
	1. 개발자가 명시적으로 정의 가능   
2. 예상이 불가능한 예외   
	1. 인터프리터 과정에서 발생하는 예외 -> 개발자 실수   
	2. 리스트의 범위가 넘어가는 값   
	3. 0으로 나누기   

### Exception Handling   
#### -1. try ~ except  

```python   
try:
	예외 발생 가능 코드   
except <Exception Type>:
	예외 발생시 대응하는 코드   
```   

위에서 제시된 try~except방법은 try내부의 코드가 진행될 때, except에서 제시한 예외상황이 생긴다면 **예외 발생시 대응하는 코드**로 넘어가 해당 예외를 처리하게 된다.    

#### -2. try ~ except ~ else   

```python   
try:
	예외 발생 가능 코드   
except <Exception type>:
	예외 발생시 대응하는 코드   
else:
	예외 발생이 하지 않았을 때 동작하는 코드   
```   

위에 제시된 형식의 경우에는 1번의 경우에서 **만약 예외가 발생하지 않았다면 else내부의 코드를 동작**할 수 있게 처리한 형식이다.   

#### -3. try ~ except ~ finally   

```python   
try:
	예외 발생 가능 코드   
except <Exception type>:
	예외 발생시 대응하는 코드
finally:
	예외 발생 여부와 상관없이 실행   
```   

위에 제시된 형식은 **예외가 발생했던 하지 않았던 finally구간**의 코드를 실행시킨다.   

#### -4. raise   
-필요에 따라 강제로 exception을 발생시킨다.   

```python   
raise <Exeption Type>(예외 정보)   
```   

#### -5. assert  
-특정 조건에 만족하지 않을 경우 예외가 발생한다.   

```python  
assert 예외 조건
# assert isinstance(decimal_number, int)
```   

### Type of Exception   

**Built-in Exception에 대해 알아보자.**   

| Exception | Contents |
|:--------:|:--------|
|   **IndexError**     | List의 index 범위를 넘어갈 때        |
|   **NameError**     | 존재하지 않은 변수를 호출할 때       |
|   **ZeroDivisionError**     |    0으로 숫자를 나눌 때    |
|   **ValueError**     |  변환할 수 없는 문자/숫자를 변환할 때      |
|   **FileNotFoundError**     |     존재하지 않는 파일을 호출할 때   |    

## 2. File  
OS에서는 파일을 **<span style="color:hotpink">트리구조</span>**로 저장하여 관리한다.   

### File VS Directory?   
#### Directory   
- 폴더 혹은 디랙토리라고 불린다.  
- 파일과 다른 디렉토리를 포함할 수 있다.   

#### File?   
- 컴퓨터에서 정보를 저장하는 논리적 단위이다.   
- 파일은 파일명과 확장자로 식별된다.   
- 실행, 읽기, 쓰기 등을 할 수 있다.   

##### 파일의 종류   

| Binary | Text |
|:--------|:--------|
| - 컴퓨터만 이해할 수 있는 형태인 이진 형식으로 저장된 파일       | - 인간도 이해할 수 있는 형태인 **문자열 형식**으로 저장된 파일        |   
| - EXCEL, WORD| - 메모장, HTML|   

##### Python File   

```python   
f = open("<파일 이름>", "접근 모드")
f.close   
```   

| 파일 접근 모드 |  설명|
|:--------:|:--------|
| r       | 읽기 모드 - 파일을 읽기만 할 때 사용       |
|  w      | 쓰기 모드 - 파일에 내용을 쓸 때 사용       |
|   a     | 추가 모드 - 파일의 마지막에 새로은 내용을 추가 시킬 때 사용 |   

```python   

f = open("test.txt", r)

with open("text.txt", r) as my_file:
	my_file을 사용하는 코드 작성
	my_file.readline() #실행시 한줄씩 읽어오기
    my_file.readlines() #파일전체를 읽어서 list로 반환한다.  
    
open("text.txt", 'r', encoding='utf8') #파일을 utf8로 인코딩하여 읽어온다.  


inport os  

if not os.path.isdir("log"):
	os.mkdir("log") #현재 폴더에 log라는 디랙터리가 없으면 만든다.  
    
    
import pathlib   

cwd = pathlib.Path.cwd() #현재 위치에대한 객체 생성

cwd.parent #현재위치에서 상위 위치의 주소 반환  
cwd.parents #현재 위치에서 모든 상위 폴더 리스트 반환  

```   

##### Pickle   
- 파이썬의 객체를 영속화하는 built-in 객체   
- 데이터, object등 실행중 정보를 저장한다. --> 불러와서 사용가능   
- 저장해야하는 정보, 계산 결과(모델)등 활용이 많이 있다.   

```python   
import pickle   

f = open("list.pickle", "wb")   #바이너리 형식으로 적는다.  

test = [1, 2, 3,4, 5]
pickle.dump(test, f)
f.close()

f = open("list.pickle", "rb")
p = pickle.load(f)
f.close
```   


## 3. log   

- 기록을 print로 남기는 것도 가능하나 Console창에만 남기는 기록은 분석시 사용 불가하다.   
- 각각의 접금권한, 용도 등에 따라 기록을 남길 필요도 있다.   

```python   
import logging  

logging.debug("디버그")   
logging.info("인포")   
logging.warning("조심해!")   
logging.error("에러남!!")    
logging.critical("와..우...")   

```   

| level | 개요 | 예제 |
|:--------:|--------|--------|
|   **debug**     |    개발시 처리기록을 남겨야하는 로그 정보를 남긴다.    |  - 다음 함수로 A를 호출한다. <br> - 변수 A를 무엇으로 변경함  |
|   **info**     | 처리가 진행되는 동안의 전보를 알림       | - 서버가 시작됨 <br> - 서버가 종료됨|
|   **warning**     | 사용자가 잘못 입력한 정보나 처리는 가능하나 원래 개발시 의도치 않는 정보가 들어왔을 때 알림       | - string 입력을 기대했으나 int가 들어옴 --> str casting으로 처리함|
|   **error**     |  잘못된 처리로 인해 에러가 났으나, 프로그램은 동작할 수 있음을 알려준다.      | - 파일에 기록을 해야하는 데 파일이 없음 -->Exception 전처리후 사용자에게 알림|
|   **critical**     | 잘못된 처리로 데이터 손실이나 더 이상 프로그램이 동작할 수 없음을 알린다.       | - 잘못된 접근으로 해당 파일이 삭제됨 |   


### 그외 실제 프로그램을 실행할때 필요한 것들   

- 데이터 파일 위치, 파일 저장장소, Operation type등을 어떻게 지정해서 프로그램이 알수 있도록할까?   

config 파일, argument등에 대해 알아보고 더불어 configparser, argparser등에 대해 알아보자.   


## 4. Data Handling  

우리는 파이썬으로 파일을 다루려고 하면 그 파일의 확장자에도 신경쓸 필요가 있다.   

| 확장자 | Contents |
|:--------:|--------|
|   **CSV**     | - 필드를 쉼표로 구분한 텍스트 파일이다. <br> - 일반적으로 textfile을 처리하듯이 파일을 읽어와서 한줄씩 처리한다. <br> - 파이썬에서는 CSV 모듈이 존재해 해당 모듈로 파일을 다룰 수 있다.        |
| **web** | - 우리는 간혹 웹페이지를 파싱해서 데이터를 수집해야할 때가 있다. <br> - 정규표현식을 사용한다면 보다 간편하게 핸들링 할 수 있다. <br> - 정규표현식을 사용하기 위해서는 re 모듈을 사용하면된다. <br> [정규표현식 in 위키](https://ko.wikipedia.org/wiki/%EC%A0%95%EA%B7%9C_%ED%91%9C%ED%98%84%EC%8B%9D)|
| **XML** | - 데이터의 구조와 의미를 설명하는 TAG를 사용하여 표시하는 언어이다. <br> -HTML과 문법이 비슷하다. <br> 컴퓨터강의 정보를 주고 받기 유용한 저장방식이다. <br> beautifulsoup으로 파싱이 가능하다. |
| **Json** | - javaScript Object Notation <br> - Java Script의 데이터 객체 표현방식 <br> - 간결성으로 기계/인간이 모두 이해하기 편하다. <br> - 데이터 용량이 적고, Code로 변환이 쉽다. <br> - 데이터의 저장 및 읽기는 dict타입과 상호호환 가능하다. |    


## 5. 그외 이모저모   
1. 강의  
- 실제 실행하는 프로그램을 개발할 때 무엇이 필요한지 공부할 수 있어 좋았다.   
2. 마스터 세션   
- 최성철 교수님께서 해주시는 여러 조언들과 이야기들은 공부를 하는데 있어 혹은 살아가는데 있어 도움이 많이 될 것같다.   
3. 피어 세션  
- 학습방법에 대해 조금 방향을 바꾸게 되었다. 하지만 바뀌게된 방법도 재미있을 것 같아 기대된다.
