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
+ 선택 정렬 (Selection Sort)
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
|인덱스|0|1|2|3|4|5|6|7|8|9|   
|요소|33|55|37|19|4|48|56|26|61|79|




