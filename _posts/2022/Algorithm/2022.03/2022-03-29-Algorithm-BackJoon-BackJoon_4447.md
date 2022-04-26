---
title: BackJoon Algorithm 4458 좋은놈 나쁜놈
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 좋은놈 나쁜놈
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-03-29 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/4447_1.png)
![alt](/assets/images/post/Algorithm/4447_2.png)


## 풀이

* charAt() 메서드로 하나씩 읽어 goodcount badcount에 각각 개수를 ++한다.

```java
import java.util.Scanner;

public class Back_4447 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        //given
        int HeroNum=sc.nextInt();
        sc.nextLine(); 
        //for안에 있는 sc.nextLine()가 반응하게 되어서 공백값으로 입력을 받는다.
        String str[]=new String[HeroNum];


        for(int i=0;i<HeroNum;i++){
            str[i]=sc.nextLine();
        }

        for(int i=0;i<HeroNum;i++) {
            int goodCount=0;
            int badCount=0;
            for(int j=0;j<str[i].length();j++){
                if(str[i].charAt(j)=='g'||str[i].charAt(j)=='G'){
                   goodCount++;
                }
                else if(str[i].charAt(j)=='b'||str[i].charAt(j)=='B'){
                    badCount++;
                }
                else{
                    continue;
                }
            }
            if(goodCount>badCount){
                System.out.println(str[i]+" is GOOD");
            }
            else if(goodCount<badCount){
                System.out.println(str[i]+" is A BADDY");
            }
            else{
                System.out.println(str[i]+" is NEUTRAL");
            }

        }


        sc.close();
    }
}


```

