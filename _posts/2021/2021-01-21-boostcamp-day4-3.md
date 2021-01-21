---
title: "[BoostCamp] DAY4 파이썬 기초 문법#3"
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

# [BoostCamp] DAY4 파이썬 기초 문법#3
---   
## 1. Python OOP   
**OOP? Object-Oriented Progrmming의 약자로서 객채지향 프로그래밍을 의미한다.**   
### 1.Class & Object   
- 객체란? 실생활에서 일종의 물건이다. --> **속성(Attribute)와 행동(Action)을 가진다.**   
	- 속성 : 변수 (variable)   
	- 행동 : 함수 (method)  
- OOP는 Class + Instance로 구성되어 있다.   
	- Class : 설계도 	
	- Instance : 실제 구현체   

#### 1) Class 구현 in Python   
##### - 1. class 선언   

![image](https://user-images.githubusercontent.com/68745983/105326545-33e86600-5c11-11eb-9b70-e90e82a962b6.png)   
> ※ 알아두면 좋아요!!
> **Python naming rule**
> **snake_case** 
> - 띄워쓰기 부분에 "_"사용
> - 파이썬 함수, 변수 명에 사용
> ex) test_case
> **CamelCase** 
> - 띄워쓰기 대신 띄어쓰기 앞 문자 대문자로 표기   
> - 파이썬 class명에 사용한다.   

##### - 2. Attribute 선언하기   
우선, 객체를 초기화하기 위해 ```__init__```을 정의해주자.   
> ※ 알아두면 좋아요!!   
> __   
> - 특수한 예약 함수나 변수 그리고 함수명 변경으로 사용한다.
> ex) ```__main__```, ```__add__```, ```__str__```, ```__eq__```   

```python   
def MyClass():   
	def __init__(self, name):
    	self.name = name  #name Attribute 즉, 변수
        
```   

##### - 3.method 구현하기   
method구현은 기존의 함수 구현과 동일하나, **self**를 추가해야만 class함수로 인정된다.   

```python
class MyClass():
	def change_my_name(self, name):
    	print("이름을 {}에서 {}로 변경합니다".format(self.name, name))
        self.name = name
```   

##### - 4.object(instance) 사용하기   

```python   
my_class = MyClass("Tumblery")  
print("현재 나는 {}입니다".format(my_class.name))
my_class.change_my_name("happyBeagle")  
print("현재 나는 {}입니다".format(my_class.name))
```   

#### 2) OOP의 특징   
##### - 1.Inheritance 상속   
부모클래스로 부터 속성과 Method를 물려받은 자식 클래스를 생성하는 것   
![image](https://user-images.githubusercontent.com/68745983/105349492-20e38f00-5c2d-11eb-9895-201b28dead4c.png)   
새는 조류의 특성을 가져온다.   
이것을 **상속**이라고 한다.   

```python   
class Birds():
	def __init__(self, feather_color):
    	self.feather_color = feather_color
        
    
    def about_me(self):
    	print("저는 조류이며 저의 깃털 색은 {}이에요.".format(self.feather_color))
        
        
class Bird(Birds):   
	def __init__(self, feather_color, species):
    	super().__init__(feather_color)
        self.species = species
        
    def about_me(self):
    	super().about_me()
        print("저는 조류과의 {}에요".format(self.species))

```   

##### - 2.Polymorphism 다형성   
- 같은 이름 메소드의 내부 로직을 다르게 작성한다.
- 파이썬에서는 Dynamic Typing 특성으로 인해 같은 부모 클래스의 상속에서 주로 일어난다.   

```python   
class Animal:
	def __init__(self, name):
    	self.name = name
    
    
    def talk(self):
    	raise NotImplementedError("Subclass must implement abstract method")
        
class Cat(Animal):
	def __init__(self, name):
    	super().__init__(name)
        
       
    def  talk(self):
    	print("냐옹")
        
        
class Dog(Animal):
	def __init__(self, name):
    	super().__init__(name)
    
    
    def talk(self):
    	print(멍멍)
        
```   

##### - 3.Visibility 가시성    
- 객체의 정보를 볼 수 있는 레벨을 조절   
- 누구나 객체 안의 모든 변수를 볼 필요가 없다.   
	- 객체를 사용하는 사용자가 임의로 정보 수정
	- 필요없는 정보에는 접근할 필요 X
	- 코드를 보호할 필요도 있음   


> ※ 알아두면 좋아요!!   
> **Encapsulation**   
>  - 캡슐화 혹은 은닉이라고 한다.   
>  - Class를 설계할 때, 클래스 간 감섭/정보 공유의 최소화   

```python   
class Inventory(object):
	def __init__(self):
    	self.__items = []    
    
    @property    #decorator
    def items(self):
    	return self.__items   
        
```  

- Inventory class에서 item객체 앞에 보면 `__`이 있다.  
	- 앞에만 `__`이 존재한다면 private로 정의한 것이다.
	- 그렇다면, 외부에서는 item에 접근이 불가능하다.   
	- 하지만 item객체의 내용을 알고 싶다면 어떻게 해야할까?    
- 우리는 items 메소드위에 **@property**라는 표현을 볼 수 있다.  
	- 이것이 숨겨진 변수를 반환하게 해주는 property decorator이다.   

###### Decorate   
java에서의 annotation과 같은 역할을 한다.  
파이썬은 함수형 언어이다.  
즉 파이썬의 함수는 일급함수라는 특성을 가진다.  

> ※일급함수?  
> - 변수나 데이터 구조에 할당이 가능한 객체
> - 매개 변수로 전달이 가능하며 리턴값으로도 사용가능하다.  
      
      
> ※ closure?   
> inner function을 return값으로 반환한다.  

```python   
def print_msg(msg):
	def printer():
    	print(msg)
    return printer  
    
``` 

그렇다면 decorator도 만들수 있을 까?   

```python
def star(func):
	def inner(*args):
    	print("*"*30)
        func(*args)
        print("*"*30)
   	return inner 
    
@star
def printer(msg):
	print(msg)
```  

그런데 decorator에도 매개변수가 존재할 수 있을까?   

```python  
def my_power(e):
	def wrapper(f):
    	def inner(*args):
        	result = f(*args)
            return e**result
        return inner
    return wrapper

@my_power(2)
def raise_two(2):
	return n**2
```   

## 2. Module & Project   
파이썬은 대부분의 라이브러리가 이미 다른 사용자에 의해 구현되어있다.  
**그런데 어떻게 사용을 할 수 있을 까?**  

### 1) Module & Package   
#### - 1.Module   
- 어떤 대상의 부분 혹은 조각이다.  
- 주로 레고 블록, 벽돌에 자주 비유된다.   
- 프로그램에서는 작은 프로그램 조각들을 일컫는다.  
ex)파이썬 built-in Module,

##### 모듈을 만들어 보자.  
- 파이썬에서 모듈은 .py 파일을 의미한다.   

**my_calc.py**   

```python   
def my_calc(a, b, c):
	return (a + b) * c
```   

이제 해당 모듈과 같은 디렉터리내에서 새로운 .py파일을 생성해서 작성해보자.   

```python   
import my_calc as c   

c.my_calc(1, 2, 3)
```  

- 모듈 안에는 함수와 클래스등이 존재가능하다.   
- 필요한 내용만 골라서 호출 가능하다.  

> ※알아두자!!  
> Built-in Module?  
> - 파이썬이 제공하는 기본 라이브러리이다 
> - 별다른 조치없이 import문으로 활용가능하다.  

#### - 2.Package   
- 모듈을 모아놓은 단위, 하나의 프로그램을 말한다.  
- 다양한 모듈들의 합이다. 폴더로 연결된다.   
- ```__init__```, ```__main__```등 키워드 파일명이 사용된다.  
- 다양한 오프손스들이 패키지로 관리된다.   

![image](https://user-images.githubusercontent.com/68745983/105358187-2fd03e80-5c39-11eb-9502-a30ee5336223.png)   
위와 같은 구조를 가진 package가 있다고 생각해보자.   

1. 폴더별로 구현된 ```__init__.py```는 무엇일까?   
	- 현재 폴더가 패키지임을 알리는 초기화 스크립트이다. 
	- 원래는 없을 경우 패키지로 생각하지 않으나 3.3부터는 그렇지 않다.   
	- 하위폴더와 py파일을 모두 포함한다.  
	- import와 ```__all__```키워드를 사용한다.   

	```python 
	__all__ = ['calc', 'validator', 'type']

	from . import calc   
	from . import validator   
	from . import type  

	```    
    
2. ```__main__.py```는 무엇일까?   
파이썬에서 package를 실행시킬때, main으로 실행되는 파일이다.   


## 3. 이모저모   
- 강의  
	- 재미있었다. 평소 파이썬에 대해 어느정도 안다고 생각했지만 중간중간 세심하게 하나씩 설명해주시는 데에서 알게되는 부분이 있는 것이 재미있었다.  

- 피어 세션   
	- 개인 공부를 하고 싶은 분들과 프로젝트를 하고 싶은 분들로 나뉘었다.  
	- 나는 프로젝트를 하기로했는데 많은 것을 얻어갈 수 있었으면 좋겠다.  
	- 같이 발전하는 경험이 되었으면 좋겠다.
