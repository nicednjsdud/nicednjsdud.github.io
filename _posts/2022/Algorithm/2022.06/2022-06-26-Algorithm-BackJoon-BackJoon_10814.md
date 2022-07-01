---
published: true
title: BackJoon Algorithm 10814 나이순 정렬 (Java)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 나이순 정렬
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-06-26 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/10814.png)


## 풀이

* Person 객체의 나이와 이름을담아서 비교해본다.

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.Comparator;
import java.util.StringTokenizer;

public class Back_10814 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();
        StringTokenizer token;
        int member_count = Integer.parseInt(br.readLine());   // 회원의 수 입력
        Person[] p = new Person[member_count];
        // when
        for(int i=0;i<member_count;i++){
            token = new StringTokenizer(br.readLine()," ");
            int age = Integer.parseInt(token.nextToken());
            String name=token.nextToken();
            p[i]=new Person(age,name);  // Person 객체에 나이,이름삽입
        }
        Arrays.sort(p, Comparator.comparingInt(s -> s.age));   

        // then
        for(int i=0;i<member_count;i++){
            sb.append(p[i].age+" "+p[i].name+"\n");
        }
        System.out.println(sb);
    }
    public static class Person{
        int age;
        String name;

        public Person(int age,String name){
            this.age=age;
            this.name=name;
        }


    }

}



```



