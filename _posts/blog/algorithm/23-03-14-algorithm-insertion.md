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
## 4_ [시간복잡도] 번외
## 5_ 최종코드