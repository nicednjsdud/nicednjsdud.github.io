---
title: BackJoon Algorithm 10698 Ahmed Aly
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: Ahmed Aly
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-04-27 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/10698.png)



## 풀이

* BufferedReader 클래스를 사용해 보았다.

* 영어문제여서 조금 당황햇지만 핵심만 집어보니 아들이 수학을 배우는데   
  틀린지 맞는지 체크해 달라는 문제이다.
 

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_10698 {
    public static void main(String[] args) throws Exception{

        //given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int T = Integer.parseInt(br.readLine()); // 테스트 케이스 입력

        //when
        for(int i=0;i<T;i++){
            StringTokenizer token = new StringTokenizer(br.readLine());
            int num1 = Integer.parseInt(token.nextToken());
            String str = token.nextToken();
            int num2 = Integer.parseInt(token.nextToken());
            String str2 = token.nextToken();
            int num3 = Integer.parseInt(token.nextToken());
            //then
            if(str.equals("+")){
                if(num1 + num2 == num3){
                    System.out.println("Case "+(i+1)+": YES");
                }
                else{
                    System.out.println("Case "+(i+1)+": NO");
                }
            }
            else if(str.equals("-")){
                if(num1 - num2 == num3){
                    System.out.println("Case "+(i+1)+": YES");
                }
                else{
                    System.out.println("Case "+(i+1)+": NO");
                }
            }
        }
        br.close();

        

    }
}


```


