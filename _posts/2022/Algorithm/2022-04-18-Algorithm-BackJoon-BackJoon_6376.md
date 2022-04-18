---
title: BackJoon Algorithm 6376
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: e 계산
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-04-18 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FraB8y%2FbtqDn2y4sHe%2FH0zq3v6AzIvTDXMrItHrk1%2Fimg.png)
![alt](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FditkfI%2FbtqDkAEhTZr%2F9yFsG4auLHDZldHStWtKq1%2Fimg.png)



## 풀이

* 시그마와 팩토리얼을 합한 문제이다. 1 부터 출력하면 값이 전부 무한대가 나오기때문에  
  초기값을 2까지 계산한값을 대입하고 시작한다. 


```java
public class Back_6376 {
    public static void main(String[] args) {

        double factorial = 2;
        double i = 2;
        double result = 2.5;
        System.out.println("n e");
        System.out.println("- -----------");
        System.out.println("0 1");
        System.out.println("1 2");
        System.out.println("2 2.5");

        for(int k=0;k<10;k++){
            factorial++;
            i *= factorial;
            result += 1/i;
            System.out.printf("%.0f %.9f\n",factorial,result);
        }

    }
}
```

