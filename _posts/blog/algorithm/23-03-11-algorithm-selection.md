---
layout: post
title: '[Sort]선택정렬 Selection'
subtitle: 선택정렬 Selection Sort 
categories:
    - blog
    - algorithm
tags:
    - sort
comments: true
published: true
---

## [Sort]선택정렬 Selection
* toc
{:toc}   

***정렬의 종류***    
+ <span style="color:green;font-weight:bold">선택 정렬 (Selection Sort) - 현재 게시글</span>
+ 버블 정렬 (Bubble Sort)
+ 삽입 정렬 (Insertion Sort)
+ 퀵 정렬 (Quick Sort)
+ 병합 정렬 (Merge Sort)
+ 힙 정렬 (Heap Sort)
<br>

# 선택 정렬 (Selection Sort)
---
## 0_개요
---
***선택 정렬은 맨 앞의 요소부터 순차적으로 최솟값만을 찾아서 정렬한다.***   
선택 정렬은 가장 **단순한 정렬 알고리즘**으로 최악의 효율을 지니고있다.   
__시간복잡도는 n^2__
진행할수록 배열의 앞쪽요소는 정렬된다. 


## 1_ 준비하기
---
***숫자 1부터 100까지 무작위로 10개 뽑는 코드.py***
```python
# main.py
import random as num              # random 함수사용을 위한 import

num_list = []                     # 비어있는 리스트 선언

while len(num_list) < 10:         # 리스트의 크기가 10개가 될 때까지 반복

    # randrang(start, stop, step) - 어디부터 어디까지 숫자 몇 간격으로 무작위를 뽑겠다
    temp = num.randrange(1,101,1) # 무작위로 1~100까지 뽑아서 temp 임시변수에 삽입

    if temp in num_list:          # 해당 값이 리스트안에 있다면 패스
        continue
    else:
        num_list.append(temp)     # 없다면 리스트에 삽입

print(num_list) # 무작위로 섞인 10가지 숫자 출력
```

## 2_ [Code] 선택정렬
```python
# selection.py
def sort(num_list):             # 위(main.py)에서 생성한 list를 매개변수로 받아온다.

    #첫번째 반복문
    #num_list의 크기만큼 반복을 한다.
    for i in range(len(num_list)): 
        min_index = i # 첫번째 반복문이 실행될 때마다 현재 위치의 INDEX값을 저장한다.

        #두번째 반복문 시작
        #첫번째 반복문의 인덱스값의 +1 한 위치부터 반복을 시작한다.
        for j in range(i+1, len(num_list)):

            #만약 리스트의 현재위치(j번째)의 값이 최소값이 있는 위치의 값보다 작을경우
            if num_list[j] < num_list[min_index]: 
                min_index = j # 현재위치(j번째) INDEX를 min_value에 저장한다.

        #두번째 반복문 끝
        #이때 리스트의 i번째보다 작은 값을 가진 인덱스값(min_index)이 정해진다.

        min_value = num_list[min_index] # 서로 위치를 바꾸기 위한 임시변수
        #min_value에 num_list의 최솟값이 있는 INDEX를 이용하여 값을 저장한다.

        # 최솟값과 현재값(i번째의 값)을 바꿔주는 과정
        num_list[min_index] = num_list[i]
        num_list[i] = min_value
    print(num_list) # 정렬된 10가지 숫자 출력
```

## 3_ [Debug] 동작설명
***3-0) num_list[10]***

|0|1|2|3|4|5|6|7|8|9|
|---|---|---|---|---|---|---|---|---|---|
|33|55|19|37|4|48|56|26|61|79|

> 첫번째 줄 인덱스, 두번째 줄 무작위 요소   
> 맨 처음 실행시 0번 요소부터 시작.   
> **위의 표는 무작위 10개의 난수로 위 코드 실행 시 다를 수 있습니다.**

<br>

***3-1) 첫번째 반복문 : i는 0부터 num_list의 크기(<10)까지 반복***
```python
for i in range(len(num_list)): 
        min_index = i 
```
**설명**   
실행시 i번의 값을 min_index에 저장한다.
> min_index = 0 [반복할때마다 1씩 증가하여 num_list의 최대길이(9)까지]

<br>

***3-2) 두번째 반복문 : j는 i+1부터 num_list의 크기(<10)까지 반복***
```python
for j in range(i+1, len(num_list)):
            if num_list[j] < num_list[min_index]: 
                min_index = j
```
**설명**   
1. 최초 실행시에는 i=0 -> min_index에 저장이 되어 두번째 반복문에서는 j=i+1 -> j=0+1 된다.   
2. **num_list[j] < num_list[min_index]** 이는   
    2-1. **num_list[1] < num_list[0]** 즉,   
    2-2. **55 < 33** 이와 같다.
3. 2-2 결과가 **<span style="color:red">False</span>** 이므로 다시 두번째 반복문으로 시작한다.
4. 조건이 될 때까지 반복문은 증감하며 계속 실행이 되므로 j는 1이 증가하여 j=0+1+1, 즉 2가 된다.
5. **num_list[j] < num_list[min_index]** 이는
    5-1. **num_list[2] < num_list[0]** 즉,   
    5-2. **19 < 33** 이와 같다.
6. 5-2 결과가 **<span style="color:blue">True</span>** 이므로 현재 j의 위치를 min_index에 저장해준다.
7. 위와같이 num_list의 길이만큼 반복한다.

> Why, 두번째 반복문은 i+1부터 시작하나요?   
> >두번째 반복문은 i번째(or min_index)의 위치한 값보다 작은 값을 찾는 코드이므로 i번째부터 시작할 경우 문제가 생길 요지가 있어 다음 요소부터 시작한다.

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
개요에서 말했듯이 시간복잡도는 최선, 평균, 최악이 모두가 **n^2**이다.   
num_list의 길이를 **50,000**로 설정을 하고 1부터 50,000까지 무작위 수를 정렬할때 걸린 시간은 <span style="color:red;font-weight:bold">71.77786 sec</span>이다. 이것보다 더 오래 걸릴 수도 있고, 낮은 수의 요소들이 앞쪽에 배치되어있다면 이것보다 덜 걸릴 수도있다.


## 5_ 최종코드



~~~python
num_list = []
while len(num_list) < 10:
    temp = num.randrange(1,101,1)
    if temp in num_list:
        continue
    else:
        num_list.append(temp)
print(num_list)
for i in range(len(num_list)):
    min_index = i
    for j in range(i+1, len(num_list)):
        if num_list[j] < num_list[min_index]:
            min_index = j

    min_value = num_list[min_index]
    num_list[min_index] = num_list[i]
    num_list[i] = min_value
print(num_list)
~~~

## 6_ 자바 Selection Sort 코드

[Java코드](https://mmmmins.github.io/blog/code/2023-03-14-code-sort/)