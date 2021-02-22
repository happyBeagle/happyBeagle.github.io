---
title: "[BoostCamp] DAY3 파이썬 기초 문법#2"
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

# [BoostCamp] DAY3 파이썬 기초 문법#2
---   
## 1.Data Structure   
### stack & queue   
#### 1. stack   
하노이 탑쌓기라는 문제를 접해 본적 있다면 이미 **Stack**을 경험 해본것이다.   
스택은 **Last In First Out (LIFO)**의 특징을 가지고 있다.  
즉, 나중에 들어간 데이터가 먼저 나온다는 것이다.   
- PUSH : data를 스택에 입력한다.
- POP  : 가장 나중에 들어간 data를 스택에서 출력한다.   
![image](https://user-images.githubusercontent.com/68745983/105127393-2bfec800-5b24-11eb-92ad-3918c1594d80.png)   
그렇다면 Python에서는 어떻게 stack을 구현할 수 있을 까   

```python   
a = [1, 2, 3, 4, 5]   #원래 stack에 1, 2, 3, 4, 5가 들어 있다고 하자.
a.append(5)  #push(5)   
a.append(6)  #push(6)   

a.pop()      #pop() --> 6출력   
a.pop()      #pop() --> 5출력   
```   

#### 2. queue   
큐는 **First In First Out (FIFO)**의 특징을 가지고 있다.   
즉, 먼저 들어간 데이터가 먼저 나온다는 것이다.   
- PUSH : data를 큐에 입력한다.
- POP  : 가장 먼저들어간 data를 큐에 입력한다.
![image](https://user-images.githubusercontent.com/68745983/105128171-da573d00-5b25-11eb-9f83-065764cfc50c.png)   
그렇다면 Python에서는 어떻게 Queue를 구현할 수 있을 까   

```python   
a = [1, 2, 3, 4, 5]   #원래 queue에 1, 2, 3, 4, 5가 들어 있다고 하자.
a.append(5)  #push(5)   
a.append(6)  #push(6)   

a.pop(0)      #pop() --> 1출력   
a.pop(0)      #pop() --> 2출력   
```   

### tuple & set   
#### 1.tuple
- **값의 변경이 불가능한 자료 구조이다.**   
- 리스트의 연산, 인덱싱 등의 연산을 동일하게 사용할 수 있다.   
- **Why Using this?**   
	- 프로그램의 작동 동안 변하지 않는 데이터를 저장한다.   
	- 혹시 모를 사용자의 실수를 미연에 방지할 수 있다.
- 어떻게 사용할 까?   

```python   
a = (0) #하나의 정수로 인식한다.
a = (0, ) #튜플의 크기가 1인 경우 ,를 붙여주도록 하자.  
```   

#### 2.set   
- 값을 순서없이 저장한다.
- 중복이 허용되지 않는다.   

```python   
s = set({1, 2, 3, 4})  	# set함수를 사용해서 set 객체를 생성한다.
						# [1, 2, 3, 4]를 set객체에 넣어 초기화해준다.   

s.add(5)				#5를 set객체에 추가한다.   
						#만약 1, 2, 3, 4와 같은 기존에 s에 포함된 element는 추가 되지 않는다.
                        #-->중복 불허   

s.remove(1)				#1을 객체 s에서 삭제한다.   
						#s = {2, 3, 4, 5}    

s.update([6, 7, 8, 9])	#[6, 7, 8, 9]추가   
s.discard(3)			#3삭제   
s.clear()				#s 객체 비우기   
```  
##### **discard VS remove**  
1. remove 메소드는 존재하지 않는 값을 삭제하려고 시도할 경우,   
**Key Error**가 발생한다.   
2. discard 메소드는 존재하지 않는 값을 삭제하려고 시도할 경우에도 문제없이 잘 실행된다.  

##### 집합 연산   

```python   
s1 = set([1, 2, 3, 4])
s2 = set([3, 4, 5, 6])

#합집합은 어떻게 연산할까?   
s1.union(s2)			#s1과 s2를 합집합을 구한다.   

#교집합은 어떻게 연산할까?   
s1.intersection(s2)		#s1과 s2의 교집합을 구한다.   
s1&s2

#차집합은 어떻게 연산할까?   
s1.difference(s2)		#s1 - s2를 구한다.
s1 - s2   

```   

### dictionary   
- key값을 활용하여 value값을 관리한다.   
- 다른 언어의 hashTable, hashMap등 이라고 말한다.   
- {key1 : value1, key2 : value2...}으로 표현된다.   

```python   
#dictionary 생성
d = {}  	# 빈 dictionary를 생성한다.
d = dict   	# 빈 dictionary를 생성한다.
d = {"one": 1, "two":2}	# dictionary를 생성하며 {"one":1, "two":2}라고 초기화 한다.   

d.items()  	#dictionary의 데이터를 출력한다.   
d.keys()	#dictionary의 key만 출력한다.   
d.values()	#dictionary의 value만 출력한다.   
```   

### collections   
- list, tuple, dict에 관련된 Python Built-in 확장 자료 구조이다.
- 편의성,실행효율등을 사용자에게 제공한다.
```
from collections import deque
from collections import Counter
from collections import OrderedDict
from collections import defaultdict
from collections import namedtuple
```   
#### 1.dequeue   
- 스택과 큐를 합친 자료구조이다.   
- list에 비해 효율적인 저장 방식을 지원한다.   

```python   
from collections import deque  

d_list = deque()  

for i in range(1, 6):
	d_list.append(i)
# [1, 2, 3, 4, 5]
d_list.appendleft(300)		# [300, 1, 2, 3, 4, 5]   
d_list.extend([6, 7, 8]) 	# [300, 1, 2, 3, 4, 5, 6, 7, 8]   
d_list.extendleft([100, 200])	# [200, 100, 300, 1, 2, 3, 4, 5, 6, 7, 8]   

d_list.rotate(1)			# [8, 200, 100, 300, 1, 2, 3, 4, 5, 6, 7]   
d_list.rotate(-1)			# [200, 100, 300, 1, 2, 3, 4, 5, 6, 7, 8]   
```   

#### 2. orderedDict   
데이터를 입력한 순서대로 반환한다. 하지만 python 3.6부터 dict또한 입력한 순서를 보장한다.   
* dict type값을 value또는 key값으로 정렬할 때 사용가능하다.   

```python   
#key값을 기준으로 정렬   
OrderedDict(sorted(d.items(), key=lambdat: t[0])).items()

#value값을 기준으로 정렬    
OrderedDict(sorted(d.items(), key=lambdat: t[1])).items()


```   

#### 3. defaultDict   
우리가 보통 dict을 사용할 때 존재하지 않는 key값에 대한 연산을 하고자 한다면, Error가 발생한다.   
**defaultdict**은 이러한 문제를 해결해준다.   

```python    
from collections import defaultdict


d =defaultdict(lambda: 0)	# Default 값을0으로 설정한다.
```   

defaultdict(object)에서 object의 경우 **함수**로 설정되어야한다.   

#### 4.else   
그 외에도 collections에는 다양한 자료구조를 제공해주니 알아보도록 하자.!!   

## 2.Pythonic code   
파이썬 스타일의 코드를 **Pythonic code**라고 한다.   
- 파이썬 특유의 문법을 활용하여 효율적인 코드를 작성한다.   
- 그러나, 파이썬 특유의 문법뿐만 아니라, 많은 언어들의 장점을 채용해 작성한다.   

### 1.split & join   
#### split
```python
#문자열을 기준값으로 나눠서 List형태로 반환하는 함수를 짠다고 생각하자.   
# 첫번째 경우
def split_string_1(input_str, sp) :
	str_list = []
    temp = ""
    for c in input_str:
    	if c == sp:
        	str_list.append(temp)
            temp = ""
       else:
       		temp += c
    str_list.append(temp)
    
    return str_list

def split_string_2(input_str, sp):
	return input_str.split(sp)
   
```   

위의 코드들중 무엇이 더 편리해보이는 가?   
Python에서는 split이라는 메소드를 통해 원하는 기준값에 맞게 문자열을 나누어 list형태로 반환할 수 있기 때문에 위와 같이 번거로운 연산을 할 필요가 없다.   
그렇다면 과연 두 방법의 효율은 얼마나 차이 날까?
```python   
import time

def split_string_1(input_str, sp) :
    str_list = []
    temp = ""
    for c in input_str:
        if c == sp:
            str_list.append(temp)
            temp = ""
        else:
            temp += c
    str_list.append(temp)

    return str_list

def split_string_2(input_str, sp):
    return input_str.split(sp)

letter = "Yesterday All my troubles seemed so far away Now it looks as though they\'re here to stay Oh, I believe in yesterday" * 10000

st_time_1 = time.time()
split_string_1(letter, " ")
en_time_1 = time.time() - st_time_1

st_time_2 = time.time()
split_string_2(letter, " ")
en_time_2 = time.time() - st_time_2


print("split_string_1 Time : {}\nsplit_string_2 Time : {}".format(en_time_1, en_time_2))
```   
위의 코드를 실행시켜보면,    
![image](https://user-images.githubusercontent.com/68745983/105162356-dba05e00-5b55-11eb-9fae-040023c5db5a.png)   
split메소드를 이용한 방법이 더 효율적이라는 것을 알 수 있다.   

#### join   
string으로 구성된 list를 합쳐서 하나의 string으로 반환해준다.   
```python  
c_list = ['a', 'b', 'c']   
ret = "".join(c_list)   
```   
"**리스트에서 string으로 합칠때 넣을 연결자**".join(list)   

### 2.list comprehension   
- 기존 list를 사용하여 간단히 다른 list를 만드는 방법   
- 일반적으로 for + append 보다 속도가 빠르다.   

```python   
#1부터 n까지 숫자로 이루어진 리스트를 만들어 보자.   
def make_list_1(n):
	ret_list = []
    for i in range(1, n + 1):
    	ret_list.append(i)
    return ret_list


def make_list_2(n):
	ret_list = [i for i in range(1, n + 1)]
    return ret_list
```  
두 함수의 속도를 비교해보자.   
![image](https://user-images.githubusercontent.com/68745983/105163515-5d44bb80-5b57-11eb-98fb-51f0f69649df.png)   
list_comprehension 방법을 사용하는 함수가 시간이 덜 드는 것을 확인할 수 있다.   

#### 2중 for문이나 2차원 배열은 어떻게 표현할 수 있나요?   

```python   
#2중 for문 사용
list = [i + j for i in range(10) for j in range(11, 20)]
'''
for i in range(10):
	for j in range(11, 20):
    	list.append(i+j)
'''

#2차원 배열 사용   
list = [[i + j for i in range(0, 10)] for j in range(11, 20)]  
'''
for j in range(11, 20):
	temp = []
    for i in range(0, 10):
    	temp.append(i + j)
    list.append(temp)
'''
```   

### 3.enumerate & zip   
#### enumerate   
리스트의 element를 추출할 때 번호를 붙여서 추출한다.   

```python   
for idx, val in enumerate(list):
	print(idx, val)
```   

#### zip   
두 개의 list의 값을 병렬적으로 추출함   

```python   
a = ['a', 'b', 'c']   
b = ['1', '2', '3']   

for i, j in zip(a, b):
	print(i, j)
'''
a 1
b 2
c 3
'''
```   

### 4.lambda & map & reduce  
#### lambda   
- 함수 이름 없이, 함수처럼 쓸 수 있는 악명함수이다.   

```python  
#일반 함수   
def func(x, y):
	return x + y   


#lambda 함수   
f = lambda x, y: x + y
```   

**python 3에서 부터는 권장하지 않으나 여전히 많이 쓰이고 있다.**   
**WHY?**   
1. 테스트가 어렵다.   
2. 코드 해석에 어려움이 있다.   
3. 이름이 존재하지 않는 함수가 나타난다.   

**※if filter사용**   
```python   
f1 = lambda x : x ** 2 if x%2 == 0    

f2 = lambda x : 1 if x % 2 == 0 else 0
```   

#### map   
map(function, list)의 형식으로 사용가능하다.    
리스트로부터 원소를 하나 씩 꺼내서 함수에 적용시킨다음, 새로 리스트를 업데이트 해주는 메소드이다.   
```python   
list = [1, 2, 3, 4]   
list_after = list(map(lambda x : x + 1, list))
#python 3에서는 iteration을 생성해주기 때문에 list로 casting을 해줘야한다.
'''
list : [1, 2, 3, 4]
list_after : [2, 3, 4, 5]
'''
```   

#### reduce   
연속된 자료형을 누적하며 연산한다.   
```python 
from functools import reduce  

a = reduce(lambda x, y: y + x, "abcde")   
```
위의 연산을 한번 생각해보자.   

| idx |calculate| status |
|:--------:|:--------:|:--------:|
|     0   | 'b' + 'a'| 'ba'|
|1|'c' + 'ba'|'cba'|
|2|'d' + 'cba'|'dcba'|
|3|'e' + 'dcba'|'edcba'|   

즉 누적하며 lambda연산을 하니 'edcba'라는 결과 값이 나온다.   

### 5. Iterable & Iterator & Generator   
#### Iterable   
연속적 자료형(sequence)에서 데이터를 순서대로 추출하는 객체이다.   

#### Iterator   
next()를 호출할 때 다음 값을 생성해내는 상태를 가진 helper이다.  

#### Generator   
- Iterator의 종류 중 하나이다.   
- element가 사용되는 시점에 값을 메모리에 반환한다.   
	- `yield`라는 매직 키워드를 통해 하나의 element만 반환한다.   


```python   
#Generator expression
gen_ex = (n * n for n in range(500))
```   

- 일반적인 iterator보다 적은 메모리 용량을 사용한다.   
- 큰데이터를 처리할때 고려해서 사용해보자!!!   


### 6. function passing arguments   
#### keyword arguments   
```python   
def sum(x, y):
	return x + y   


sum(1, 2)
```    
함수에 입력되는 parameter의 변수명을 사용한다.   

#### default arguments   
```python  
def sum2(x, y = 2):
	return x + y
    
    
sum(1)
```    
입력하지 않을 경우 기본값을 출력한다.    


#### variable-length asterisk   
**variable-length**  
- 개수가 정해지지 않은 변수를 함수의 parameter로 사용한다.   
- keyword argument와 함꼐 argument 추가가 가능하다.    
- *기호를 사용하여 함수의 매개변수를 표시한다.   
- 입력된 값은 tuple type으로 사용할 수 있다.   

```python    
#가변인자는 일반적으로 *args를 변수명으로 사용한다.   
#기존 매개변수 이후에 나오는 값을 tuple에 저장한다.   
#    --> 하나만 사용가능하다.
def test(a, b, *args):
	return sum(args)
    
    
#매개변수 이름을 따로 지정하지 않고 입력해보자.   
#*를 두개 사용하여 함수의 매개 변수를 표시한다.   
#입력된 값은 dict type으로 사용가능하다.   
def test2(a, b, *args, **kwargs):
	print("First V : {first}".format(**kwargs))

```

##### *는 무슨 의미일까?   
단순 곱셈, 제곱연산, 가변인자등 다양하게 활용되는 \* 또 다른 활용이 존재할까?   
**<span style="color:red">oooo 존재한다!!!!!!!</span>**   

tuple, dict등 자료형에 들어 있는 값을 unpacking한다.   
*(1, 2, 3, 4,) = 1, 2, 3, 4    

```python   
def test(a, b, c):
	return a + b + c

data = {'a':1, 'b':2, 'c':3}
test(**data)
```   

위와 같은 예제를 보면 \**가 dict앞에 있는 경우에는 dict을 unpacking하여 그에 필요한 값을 대입한다.   
다만 이때, 매개변수에 존재하지 않는 key가 존재한다면 오류가 날 수 있다.   


## 3.이모저모   
### 오늘의 강의   
오늘 강의에서 요즘 사용되는 코딩 방식, 기존에 간과하고 넘어갔던 부분들에 대해 설명해 주셔서 좋았다.   
### 피어세션   
오늘은 피어세션을 어떻게 활용할지 고민을 해보는 시간을 가졌다.   
U, P스테이지에서 학습하는 부분뿐만 아니라 그 외적인 부분도 함께 공부하고 싶은 욕심이 생겼다.   
더 열심히 학습해야겠다.
