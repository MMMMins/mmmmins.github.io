---
layout: post
title: '[Code]선택정렬 Java'
subtitle: Code 선택정렬 Java
date: '2023-03-11 00:00:00 +0900'
categories:
    - blog
    - code
tags:
    - sort
comments: true
published: true
---

## [Code]선택정렬 Java

* toc
{:toc}

## 자바코드.java
***파이썬과 구조는 같다.***

~~~java

import java.util.Random;

public class Selection {
    public static void main(String[] args) {

        // 랜덤 시작 부분
        final int number = 1000;
        int[] numList = new int[number];

        Random ran = new Random();
        for(int i=0; i<number; i++){
            numList[i] = 0;
        }

        for(int i=0; i<number; i++){
            int temp = ran.nextInt(number)+1;
            if(numList[i] == temp){
                i--;
            }else if(numList[i] == 0){
                numList[i] = temp;
            }
        }
        for(int a : numList){
            System.out.print(a+", ");
        }
 
        // 정렬 시작 부분
        System.out.println();
        for(int i=0; i<number; i++){
            int minIndex = i;
            for(int j=i+1; j<number; j++){
                if(numList[j] < numList[minIndex]){
                    minIndex = j;
                }
            }
            int minValue = numList[minIndex];
            numList[minIndex] = numList[i];
            numList[i] = minValue;
        }

        for(int b: numList){
            System.out.print(b+", ");
        }
    }
}

~~~