---
title: BackJoon Algorithm 2846 오르막길
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 오르막길
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-03-23 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/2846.png)



## 풀이

* 오르막길이 아닐시 초기화를 해야하므로 그점을 유념해야한다.
* 오르막길은 항상 계속 증가해야한다. 그러므로 중간에 숫자가 똑같으면 초기화


```java
import java.util.Scanner;

public class Back_2846{
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        //given
        int num = sc.nextInt();
        int street[] = new int[num];
        int size = 0;
        int size_temp = 0;
        //when
        for (int i = 0; i < num; i++) {
            // 길 입력받기
            street[i] = sc.nextInt();
        }
        for (int i = 0; i < num-1; i++) {
            // 다음으로 배열이 클때 더하기
            if (street[i] < street[i + 1]) {
                size += street[i + 1] - street[i];

            }
            else {
                // 다음으로 오는 배열이 작거나 같을때 그전 size 변수에저장
                if (size_temp < size) {
                    size_temp = size;
                }
                // size 초기화
                size=0;
            }
            }
        //then
        if(size_temp>=size){
            System.out.println(size_temp);
        }
        else{
            System.out.println(size);
        }
    }
}
```

