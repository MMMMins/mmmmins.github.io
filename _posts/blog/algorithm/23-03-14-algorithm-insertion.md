---
layout: post
title: '[Sort]삽입정렬 Insertion'
subtitle: 삽입정렬 Insertion Sort 
categories:
    - blog
    - algorithm
tags:
    - sort
comments: true
published: true
---

## [Sort]삽입정렬 Insertion
* toc
{:toc}   

***정렬의 종류***    
+ 선택 정렬 (Selection Sort)
+ 버블 정렬 (Bubble Sort)
+ <span style="color:green;font-weight:bold">삽입 정렬 (Insertion Sort) - 현재 게시글</span>
+ 퀵 정렬 (Quick Sort)
+ 병합 정렬 (Merge Sort)
+ 힙 정렬 (Heap Sort)
<br>

## 0_ 개요
## 1_ 준비하기

***중복없는 랜덤 숫자 리스트 생성.py***   
```python
# main.py
import random as num              # random 함수사용을 위한 import

num_list = []                     # 비어있는 리스트 선언

while len(num_list) < 1000:         # 리스트의 크기가 1000이 될 때까지 반복

    # randrang(start, stop, step) - 어디부터 어디까지 숫자 몇 간격으로 무작위를 뽑겠다
    temp = num.randint(1,1000) # 무작위로 1~1000까지 뽑아서 temp 임시변수에 삽입

    if temp in num_list:          # 해당 값이 리스트안에 있다면 패스
        continue
    else:
        num_list.append(temp)     # 없다면 리스트에 삽입

print(num_list) # 무작위로 섞인 10가지 숫자 출력
```

## 2_ [Code] 삽입정렬

~~~python
def sort(num_list):
    # 첫번째 반복문
    # 0번째는 정렬할 때 필요가 없으므로 1번째 요소부터 시작한다.
    for i in range(1, len(num_list)):

        # 두번째 반복문
        # i번째 요소부터 0번째까지 내려가면서 정렬을 한다.
        for j in range(i,0,-1):

            # j-1번째 요소가 j번째 요소보다 크다면~
            if num_list[j-1] > num_list[j]: #현재 위치의 요소가 한칸 이전의 요소보다 작다면 정렬을 수행한다.
                temp = num_list[j-1] # 이전에 있는 요소(큰 값)를 임시변수에 저장한다.
                num_list[j-1] = num_list[j] # 한칸 이전의 위치에 현재 위치의 요소(작은 값)를 저장한다.
                num_list[j] = temp # 임시변수에 저장한 큰 값을 현재위치에 저장한다.

                # 파이썬 문법으로 가능한 것
                # num_list[j-1], num_list[j] = num_list[j], num_list[j-1]
                # 이 경우 temp 임시변수는 필요가 없다.
    print(num_list)
~~~
## 3_ [Debug] 동작설명
***3-0) num_list[10]***

|0|1|2|3|4|5|6|7|8|9|
|---|---|---|---|---|---|---|---|---|---|
|33|55|19|37|4|48|56|26|61|79|

> 첫번째 줄 인덱스, 두번째 줄 무작위 요소   
> 맨 처음 실행시 0번 요소부터 시작.   
> **위의 표는 무작위 10개의 난수로 위 코드 실행 시 다를 수 있습니다.**

<br>

***3-1) 첫번째 반복문 : i는 1부터 num_list의 크기(<10)까지 반복***
```python
    for i in range(1, len(num_list)):
```
> Why? i는 0번부터가 아닌 1번부터하는 이유는 두번째 반복문에서 j는 i의 값을 할당받는데, 이후 조건 처리시 이전 요소와 비교를 하기 때문에 1번부터한다.

<br>

***3-2) 두번째 반복문 : j는 i부터 0이 될때까지 반복***
```python
    for j in range(i,0,-1):
        if num_list[j-1] > num_list[j]: 
                temp = num_list[j-1]
                num_list[j-1] = num_list[j]
                num_list[j] = temp
```
**설명**   
1. i[len:10] 에서부터 0이 될때까지 반복한다.
2. **num_list[j-1] > num_list[j]** 이는   
    2-0. i는 1번부터 num_list의 크기만큼 시작하므로 0번째 공간비교를 위해 -1을 해준다.
    2-1. **num_list[0] > num_list[1]** 즉,   
    2-2. **33 > 55** 이와 같다.
3. 2-2 결과가 **<span style="color:red">False</span>** 이므로 다시 두번째 반복문으로 시작한다.
4. 조건이 될 때까지 반복문은 감소하며 계속 실행이 되므로 j는 1씩 감소하여
5. **num_list[j-1] < num_list[j]** 이는
    5-1. **num_list[1] < num_list[2]** 즉,   
    5-2. **19 < 33** 이와 같다.
6. 5-2 결과가 **<span style="color:blue">True</span>** 이므로 현재 j의 위치를 min_index에 저장해준다.
7. 위와같이 num_list의 길이만큼 반복한다.
.

<br>

***3-3) 두번째 반복문이 끝난 후, 최솟값의 위치와 현재 i의 위치를 이용하여 서로 값을 바꿔준다.***
```python
        min_value = num_list[min_index] 
        num_list[min_index] = num_list[i]
        num_list[i] = min_value
```
**설명**   
<span style="color:red;font-weight:bold">num_list[0]</span>에는 <span style="color:red;font-weight:bold">55</span>가 들어있고 <span style="color:blue;font-weight:bold">num_list[2]</span>에는 <span style="color:blue;font-weight:bold">19</span>가 들어있다.

서로 바꿔주기위해 <span style="color:blue;font-weight:bold">19(num_list[2])</span>를 <span style="color:green;font-weight:bold">min_value</span>에 넣어주고 <span style="color:red;font-weight:bold">55(num_list[0])</span>를
<span style="color:blue;font-weight:bold">19(num_list[2])</span>의 공간에 저장해준다.   

|변수|기존|변경|
|---|---|---|
|min_value|-|19|
|min_list[0]|55|-|
|num_list[2]|19|55|


<span style="color:red;font-weight:bold">55(num_list[0])</span>의 위치 에<span style="color:green;font-weight:bold">19(min_value)</span>를 저장해준다.

|변수|기존|변경|
|---|---|---|
|min_value|19|-|
|num_list[0]|55|19|
|num_list[2]|-|55|


> Why, min_value를 사용해야 하나요?
> > 간단한 예시로 복사 붙여넣기를 생각하면 된다. 두개의 브라우저의 주소를 각각 바꾸려고한다.    
크롬에는 <span style="color:red;font-weight:bold">A주소</span>를 
<span style="color:blue;font-weight:bold">B주소</span>로, 
사파리에는 <span style="color:blue;font-weight:bold">B주소</span>를 
<span style="color:red;font-weight:bold">A주소</span>로 바꾸려고할 때,   
<span style="color:blue;font-weight:bold">B주소</span>를 복사한 채로 크롬에 붙여 넣게되면, <span style="color:red;font-weight:bold">A주소</span>가 사라져버린다. 반대로 해도 결과는 똑같으므로 메모장 같은 곳에 <span style="color:green;font-weight:bold">한개의 주소</span>를 붙여넣고 처리를 하면 원래의 목적대로 이룰 수 있는 것과 같이, min_value의 사용 이유도 같다.

## 4_ [시간복잡도] 번외
## 5_ 최종코드