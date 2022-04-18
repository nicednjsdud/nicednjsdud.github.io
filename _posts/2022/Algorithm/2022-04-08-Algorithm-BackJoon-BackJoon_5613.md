---
title: BackJoon Algorithm 5613
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 계산기 프로그램
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-04-08 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/5613.png)
![alt](/assets/images/post/Algorithm/5613_2.png)

## 풀이

* Switch 를 이용하여 계산기를 만든다.
* =이 나오기 전까지 계산을 해야하므로 케이스안에 입력을 한번 더 넣어준다.

```java
import java.util.Scanner;

public class Back_5613 {
    public static void main(String[] args) {
        // given
        Scanner sc = new Scanner(System.in);
        int num=sc.nextInt();           // 수 입력
        int result=num;                    // 결과 담을 변수
        while(true){
            String clac=sc.next();         // 사칙연산 입력
            if(clac.equals("=")){          // 사직연산이 = 이면 종료
                System.out.println(result);
                break;
            }
            switch (clac){
                case "+":
                    int num1=sc.nextInt();
                    result+=num1;
                    break;
                case "-":
                    int num2=sc.nextInt();
                    result-=num2;
                    break;
                case "*":
                    int num3=sc.nextInt();
                    result*=num3;
                    break;
                case "/":
                    int num4=sc.nextInt();
                    result/=num4;
                    break;
            }

        }
        sc.close();
        

    }
}

```

