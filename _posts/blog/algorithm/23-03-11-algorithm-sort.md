---
layout: post
title: 'Sort (1)'
subtitle: 선택, 버블, 삽입 정렬에 대해서
categories:
    - blog
    - algorithm
tags:
    - sort
comments: true
published: true
---

## Sort [1]
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
import random as num              # random 함수사용을 위한 import

num_list = []                     # 비어있는 리스트 선언

while len(num_list) < 10:         # 리스트의 크기가 10개가 될 때까지 반복
    temp = num.randrange(1,101,1) # 무작위로 1~100까지 뽑아서 temp 임시변수에 삽입
    # randrang(start, stop, step) - 어디부터 어디까지 숫자 몇 간격으로 무작위를 뽑겠다
    if temp in num_list:          # 해당 값이 리스트안에 있다면 패스
        continue
    else:
        num_list.append(temp)     # 없다면 리스트에 삽입

print(num_list) # 출력값 [52, 54, 12, 2, 43, 8, 86, 20, 68, 71]
```
