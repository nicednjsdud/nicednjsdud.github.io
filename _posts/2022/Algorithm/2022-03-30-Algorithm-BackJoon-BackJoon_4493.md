---
title: BackJoon Algorithm 4493 가위 바위 보?
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 가위 바위 보?
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-03-30 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/4493.png)


## 풀이

* charAt() 메서드를 활용

```java
import java.util.Scanner;

public class Back_4493 {
    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);
        // given
        
        int test_count =sc.nextInt();
        // when
        for(int i=0;i<test_count;i++){              // 테스트 케이스 개수
            int count=sc.nextInt();                   // 가위 바위보를 한 횟수
            sc.nextLine();
            String str[]=new String[count];
            int P1_count=0;
            int P2_count=0;
            for(int j=0;j<count;j++){
                str[j] =sc.nextLine();
                if(str[j].charAt(0)=='R'){
                    if(str[j].charAt(2)=='P'){
                        P2_count++;
                    }
                    else if(str[j].charAt(2)=='S'){
                        P1_count++;
                    }

                }
                else if(str[j].charAt(0)=='P'){

                    if(str[j].charAt(2)=='S'){
                        P2_count++;
                    }
                    else if(str[j].charAt(2)=='R'){
                        P1_count++;
                    }
                }
                else if(str[j].charAt(0)=='S'){
                    if(str[j].charAt(2)=='P'){
                        P1_count++;
                    }
                    else if(str[j].charAt(2)=='R'){
                        P2_count++;
                    }
                }

            }
            // then
            if(P1_count>P2_count){
                System.out.println("Player 1");
            }
            else if(P1_count<P2_count){
                System.out.println("Player 2");
            }
            else{
                System.out.println("TIE");
            }

        }
    }
}

```

