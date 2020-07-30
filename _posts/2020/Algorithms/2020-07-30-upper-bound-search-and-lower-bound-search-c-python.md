---
title: Upper Bound Search and Lower Bound Search ( c++/ python)
categories:
- Algorithms
tags:
- upperBound
- lowerBound
- search
description: upper bound  search와  lower bound search에 대해 학습합니다.
layout: single
author_profile: true
read_time: true
comments: null
share: true
related: true
toc: true
toc_sticky: true
toc_label: contents
---

## Upper  Bound Search
정렬된 배열에서 target 값이 존재할 때 target 값을  <span style="color:red">초과</span>하는 값들 중 첫번째 위치를 반환한다. 
###  [1. CPP](https://github.com/happyBeagle/algorithms/blob/master/algorithms/cpp/upperBoundSearch.cpp)
```cpp
int upperBound(vector<int>& arr, int target) {
	int left = 0, right = arr.size() - 1;
	while(left < right) {
		int mid = (left + right) / 2;
		
		if(arr[mid] <= target) {
			left = mid + 1;
		}
		else {
			right = mid;
		}
	}
	return right;
}
```
### [2. Python](https://github.com/happyBeagle/algorithms/blob/master/algorithms/python/upperBoundSearch.py)
```python
def upperbound(arr: List[int], target: int) -> int:
	left, right = 0, len(arr) - 1
	
	while (left < right):
		mid = (left + right) // 2
						
		if(arr[mid] <= target):
			left = mid + 1
		else:
			right = mid
			
	return right
```

>  **Upper Bound Search**의 목적은 target의 값보다 큰 첫번째 값의 위치를 찾는 것이다. 따라서,
> ```
> arr[mid] <= target:
> 	left = mid + 1
> ```
> 위 와 같이 처리를 해주는 것은 target의 값과 비교해서 그 이하인 값을 찾았을 때,  left 값을 움직여 target의 값보다 큰 첫번째 값의 위치를 찾기 위해서이다.


## Lower Bound Search
정렬된 배열에서 target 값이 존재할 때 target 값보다 <span style="color:red">크거나 같은</span> 값들의 첫번째 위치를 반환한다.
###  [1. CPP](https://github.com/happyBeagle/algorithms/blob/master/algorithms/cpp/lowerBoundSearch.cpp)
```cpp
int lowerBound(vector<int>& arr, int target) {
	int left = 0, right = arr.size() - 1;
	while(left < right) {
		int mid = (left + right) / 2;
		
		if(arr[mid] < target) {
			left = mid + 1;
		}
		else {
			right = mid;
		}
	}
	return right;
}
```
### [2. Python](https://github.com/happyBeagle/algorithms/blob/master/algorithms/python/lowerBoundSearch.py)
```python
def lowerbound(arr: List[int], target: int) -> int:
	left, right = 0, len(arr) - 1
	
	while (left < right):
		mid = (left + right) // 2
						
		if(arr[mid] < target):
			left = mid + 1
		else:
			right = mid
			
	return right
```

>  **Lower Bound Search**의 목적은 target의 값보다 크거나 같은 첫번째 값의 위치를 찾는 것이다. 따라서,
> ```
> arr[mid] < target:
> 	left = mid + 1
> ```
> 위 와 같이 처리를 해주는 것은 target 값보다 작은 값을 찾았을 때, left값을 움직여 target의 값보다 크거나 같은 첫번째 값의 위치를 찾기 위해서이다.
