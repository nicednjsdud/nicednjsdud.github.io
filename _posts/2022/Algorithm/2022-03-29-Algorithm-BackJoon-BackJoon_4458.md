---
title: BackJoon Algorithm 4458 첫 글자를 대문자로
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 첫 글자를 대문자로
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

![alt](/assets/images/post/Algorithm/4458.png)


## 풀이

* StringBuilder 는 String과 문자열을 더할 때 새로운 객체를 생성하는 것이 아니라  
  기존의 데이터에 방식을 사용하기 때문에 속도도 빠르고 부하가 적다.
* append() 문자열을 더해주는 역할
* substring으로 문자를 잘라주고 toUpperCase() 메서드를 사용하여 대문자로 변환

```java
import java.util.Scanner;

public class Back_4458 {
    public static void main(String[] args) {
        // given
        Scanner sc=new Scanner(System.in);
        StringBuilder sb = new StringBuilder();
        int num=sc.nextInt();
        sc.nextLine();
        // when
        for(int i=0;i<num;i++){
            String temp =sc.nextLine();

            String result=temp.substring(0,1).toUpperCase()+""+temp.substring(1,temp.length());

            sb.append(result+"\n");
        }
        // result
        System.out.println(sb.toString());
        sc.close();
    }
}


```

