---
title: BackJoon Algorithm 10102 개표
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 개표
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-04-22 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/10102.png)



## 풀이

* BufferedReader 클래스를 사용해 보았다.
* if 문으로 조건을 넣으면 된다.

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;


public class Back_10102 {
    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int v = Integer.parseInt(br.readLine());  // 심사위원 수
        char ch[] = new char[v];                  // 점수 넣은 char형 배열

        for(int i=0;i<v;i++){
           ch[i]= (char) br.read();               // 하나씩 넣기
        }
        int Acount=0;                   
        int Bcount=0;
        for(int i=0;i<v;i++){

            if(ch[i]=='A'){
                Acount++;
            }
            else if(ch[i]=='B'){
                Bcount++;
            }
        }
        if(Acount>Bcount){
            System.out.println("A");
        }
        else if(Acount<Bcount){
            System.out.println("B");
        }
        else{
            System.out.println("Tie");
        }
        br.close();
    }
}
```


