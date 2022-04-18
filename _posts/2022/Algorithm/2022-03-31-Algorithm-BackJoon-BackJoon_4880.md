---
title: BackJoon Algorithm 4880 다음수
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 다음수
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-03-31 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/4880.png)


## 풀이

* 등차 수열(AP)의 경우 세 항 중 근접한 항 끼리 차이를 알아내고 차이가 똑같다면  
  이를 등차 수열(AP)로 판단한다. 판단이 되었다면 다시 다음 항은 마지막 항과 차이   
  값을 더해주면 된다.
* 이후 등비 수열(GP)로 판단한다. 이후 마지막 항에 공비를 곱해주면 된다.

```java
    import java.util.Scanner;

public class Back_4880 {
    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);
        boolean run =true;
        while(run){
            int num1=sc.nextInt();
            int num2=sc.nextInt();
            int num3=sc.nextInt();
            if(num1==0&& num2 ==0 && num3==0){
                break;
            }
            if((num3-num2)==(num2-num1)){
                // 등차수열
                int num4= num3+(num3-num2);
                System.out.println("AP "+num4);
            }
            else if((num3/num2)==(num2/num1)){
                // 등비수열
                int num4 = num3*(num2/num1);
                System.out.println("GP "+num4);
            }
        }
    }
}

```

