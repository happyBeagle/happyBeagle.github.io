---
title: "[BoostCamp] DAY2 파이썬 기초 문법"
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- BoostCamp_AI_Tech
tags:
- BoostCamp_AI_Tech
- Python
toc: true
toc_sticky: true
toc_label: contents
---

# [BoostCamp] DAY2 파이썬 기초 문법
---   
## 1.Variables & List  
### Variables
우선, 변수(variables)란 무엇일까?   
우리는 우선 `a = 10`이라는 말에 대해 고민해볼 필요가 있다.   
![image](https://user-images.githubusercontent.com/68745983/105022038-9b28dd80-5a8c-11eb-91c7-128aa8ac64eb.png)   
위의 그림을 보자.   
우리는 **메모리의 한 부분을 할당**하여  
**a라고 명명한 변수가 해당 메모리를 가르키도록 한다.**   
그리고 `a=10`을 통해 **a가 가리키는 메모리에 10을 집어 넣는다.**  

#### 변수는 어떤 규칙으로 정하나요?   

- 알파벳, 숫자, _로 선언 가능하다.  
- 변수명은 **<span style="color:blue">의미 있는 단어로 표기</span>**하자!!
- 변수명은 **<span style="color:blue">대소문자가 구분</span>**된다.
- **<span style="color:blue">특별한 의미가 있는 예약어</span>**는 쓰지 않는다.
	- ex) for, if, else 등   

#### 자료형?   
우리가 C를 사용할 때 생각해보면, 각각의 변수에는 type이 정해져있다.   
`int a = 10`   
![image](https://user-images.githubusercontent.com/68745983/105028390-5012c880-5a94-11eb-880c-7afb57308b53.png)   
##### Python에서는 어떻게 type을 정할 수 있까?   
보통 C나 JAVA등과 같은 언어들은 `int code = 10 `과 같이 변수의 자료형을 미리 정해준다.    
그렇다면 **Python**에서는 어떻게 변수의 자료형을 지정해줄까?   
**Dynamic Typing**  
변수에 넣어지는 자료에 따라 **동적으로** 자료형을 지정해준다.   
```python
a = 10 #Integer   
b = 10.0 #Float   
c = 'abc' #string   
```   
##### 자료형 변환?   
```python   
a = 10   
b = float(a) # 10.0   
c = str(a) # "10"   
type(c) #<class 'string'>
```   

#### 연산자   
+, -, /, %등을 연산자라고 한다.   
a + b와 같이 +연산을 하는데 필요한 요소들을 피연산자라고 한다.   
```python
a = 10   
b = 5   
c = 3   

#+연산 (더하기)   
num_sum = a + b   

#증가 연산   
a = a + 1 #11  
a += 1 #12   

#-연산 (빼기)   
num_minus = a - b   

#감소 연산   
a = a - 1 #11   
a -= 1 #10   

#곱셈 연산   
num_mul = a * b   
a *= b #50   

#나눗셈 관련 연산   
num_div = a / c #16.66666666...   
num_quo = a //c #16   
num_reminder = a % c #2   

```   

#### ※Float오차?   
컴퓨터에서는 소숫점을 이진수로 계산한다.   
그러면, 0.1을 이진수로 표현해보자.   

| 십진수 표현 | binary |remind(남은수)|
|:--------:|:--------:|:--------:|
|    0.5    |      0  |  0.1 |
|  0.25|0|0.1|
|0.125|0|0.1|
|0.0625|1| 0.1 - 0.0625 = 0.0375|
|0.03125|1| 0.0375 - 0.03125 = 0.00625|
||...||     

위와 같은 과정을 통해 0.1을 이진수로 표현하면 0.00011....로 표현이된다.   
그래서 간혹 아주 미세한 오차가 발생하기도 한다.   
하지만, Python 3.X에서는 정상적으로 표현된다고 한다.   



### List   
List, Array등은 다양한 자료들을 저장한 **Sequence 자료형**이다.   
#### C VS Python (feat. List)   
**1. C언어**   
```C
int nums[] = {1, 2, 3, 4};
```   
**2. Python**   
```python   
nums = [0, 1, 2.0, [1, 2, 3], "123"]
```
C언어와 Python에서 생성한 List, Array을 확인해보자.  
C는 모든 element가 하나의 자료형으로 통일되어야한다.  
하지만 python을 확인해보면, 하나의 List에 다양한 자료형이 포함되는 것이 허용되는 것을 확인할 수 있다.   

#### 배열 COPY   
```python   
a = [1, 2, 3, 4]
b = a
c = a[:]
```  
b와 c의 상태를 확인해보자.   
![image](https://user-images.githubusercontent.com/68745983/105033972-2eb5da80-5a9c-11eb-89ff-5b4d2cc9d8c8.png)  
`b = a`의 의미는 b가 a가 가르키는 메모리를 공유한다는 것이다.  
`c = a[:]`의 의미는 a를 복사하여 새로 할당된 c의 위치에 넣는 것이다.   

**그렇다면 이차원 배열은 어떻게 복사할까?**   
**1.얕은 복사**  
주소가 공유되며 해당 주소 내의 데이터를 함께 사용하는 복사   
```python   
a = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]   
b = a #shallow copy
```   
**2.깊은 복사**  
기존의 주소내의 데이터를 복사하여 새로 할당된 메모리에 그 값을 넣는 다.
즉 서로 독립적인 객체가 된다.   
```python   
import copy   
a = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]   

b = copy.deepcopy(a)   
```   

## 2. 함수와 Console I/O   
### Function  
![image](https://user-images.githubusercontent.com/68745983/105036370-bcdf9000-5a9f-11eb-9739-50d772fc5a2b.png)  
함수는 위의 그림과 같이 구성되어 진다.   
**주로 argument도 매개변수라고 명명하기도 한다.**   

#### About Parameter   
##### 1.Call by value   
매개변수를 입력할 때 값을 참조하여 가져온다.
```c
int func(int a) {   
	a += 10;   
    return a;    
}    

int main() {   
	int num = 8;
    func(num);//num = 8, return 값 18
	return 0;
}   
```
위의 예제에서 func함수에서 a+=10을 거친 a는 18이 되지만, 함수가 return된후 num의 값은 변하지 않는다.   
**즉, arument에는 영향을 주지않는다.**   

##### 2.Call by reference   
입력된 매개변수는 주소를 parameter에 넘겨주어 연산을 한다.   
```c   
int func(int& a) {
	a += 10;
    return a;
}   

int main() {
	int num = 10;   
    func(num);// num = 20  
    return 0;   
}
```
위의 예제에서 확인할 수 있듯 주소를 참조하여 연산을 하기 때문에 func함수의 연산이 끝나고 return이 되고 난 후에는 num의 값이 변경된다.   

##### 3.Call by object   
파이썬 함수에서 사용되어지는 방법이다.   
함수에 매개변수를 넘겨줄때 객체를 넘겨주는 방법이다.   
```python   
def func(a):
	a.append(1)  
    a = [1, 2, 3]
    return a   

a = [0]
func(a)
```   
위의 코드에서 func함수에서는 object를 매개변수로 넘겨 받기 때문에   
`a.append(1)`   
연산을 통해 밖의 a List에도 1이 추가됬을 것이다.   
하지만   
`a = [1, 2,3]`  
의 연산을 통해 a가 새로운 메모리를 할당받으므로 바깥의 a에는 영향을 주지 않을 것이다.   
**∴연산 후의 a = [0, 1], return 값 = [1, 2, 3]**   

### Console I/O  
#### Input   
```python   
a = input()   
b = input("input num:")   
```
input함수에 의한 return값은 string으로 반환된다.  
그러니 type변환으로 원하는 값을 구해주자.   

#### Output   
출력은 **print()**라는 함수를 이용한다.   
```C
printf("%d * %d = %d", 1, 2, 2)
```   
와 같은 표현을 python에서는 어떻게 할까?   
##### % string   
```python   
print("%d %d"%(1, 2))
```   
##### format 함수   
```python   
print("{} {}".format(a, b))
```   
##### f-string   
```python   
name = "happy beagle"
print(f"{name}")
```   

### 그외 이모저모   
1. [sring의 표현법에는 더 많은 것이있으니 찾아보도록하자.!](https://www.w3schools.com/python/ref_string_format.asp)
2. [string에는 많은 메소드, 기능들이 존재한다.](https://www.w3schools.com/python/python_strings.asp)   

* 오늘은 갑자기 수업시간이 늘어 당황했다.  
* 과제가 많이 있었으나 재미 있었다.  
* 피어세션에서 함께 공부할 것들을 찾아보자.   
	* 현재는 캐글 competition에 대해 알아보고 있다.  
		* 공부하기 좋은게 뭐가 있을까?	
* 내일도 화이팅!!!
