---
title: BackJoon Algorithm 10872 팩토리얼
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 팩토리얼
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-05-01 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/10872.png)



## 풀이

* 어느 영상에서 본 댓글인데 0!은 참이므로 0! = 1 이다라는 말도 있습니다. ㅎㅎ;
* 0! = 1로 해야 편해서 그렇게 한 거다 라는 말도 있습니다.

![alt](/assets/images/post/Algorithm/10872_1.png)

```
    1!=1(기본수)×1
    2!=1(기본수)×1×2
    then..
    0!=1(기본수)
```


![alt](/assets/images/post/Algorithm/10872_2.png)
 

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_10872 {
    public static void main(String[] args) throws IOException {


        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());                // 정수 입력
        int result=1;
        int factorial=N;
        // when
        if(N==0){
            N=1;                                                // factorial 0은 1이다.
        }
        for(int i=0;i<N;i++){
            if(factorial==0) {
                break;
            }
            result *= factorial;
            factorial--;

        }
        // then
        System.out.println(result);
    }
}


```


