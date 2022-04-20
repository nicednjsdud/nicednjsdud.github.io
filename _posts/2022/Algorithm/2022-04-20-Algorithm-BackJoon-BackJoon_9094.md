---
title: BackJoon Algorithm 9076 수학적 호기심
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 수학적 호기심
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-04-20 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/9094.png)



## 풀이

* BufferedReader 클래스를 사용해 보았다.
* StringTokenizer 클래스는 문자열을 우리가 지정한 구분자로 문자열을 쪼개준다.   
  그걸 token 이라고 한다.
* String nextToken() 는 다음의 토큰을 반환한다. (string타입을 반환) 


```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Back_9094 {
    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int test_count = Integer.parseInt(br.readLine()); // 테스트 카운트 읽기

        for(int i=1;i<=test_count;i++){
            StringTokenizer token = new StringTokenizer(br.readLine());
            int n = Integer.parseInt(token.nextToken());
            int m = Integer.parseInt(token.nextToken());
            int count =0;
            for(int a=1;a<n;a++){

                for(int b=a+1;b<n;b++){

                    if((((a*a)+(b*b)+m)%(a*b))==0){ // 나머지가 0이아니면 정수x
                        count++;                    // 정수 찾기
                    }
                }
            }
            System.out.println(count);

        }
    }
}

```


