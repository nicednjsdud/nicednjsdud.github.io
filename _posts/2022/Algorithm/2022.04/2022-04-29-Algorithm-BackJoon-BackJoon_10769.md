---
title: BackJoon Algorithm 10769 행복한지 슬픈지
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 행복한지 슬픈지
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-04-29 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/10769.png)



## 풀이

* BufferedReader 클래스를 사용해 보았다.

* ch[]배열을 하나 선언해 str 문자열을 담는다.
 

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_10769 {
    public static void main(String[] args) throws IOException {

        // given
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        String str = br.readLine();           // 문자열 입력
        int happycount=0;                     // happy 카운트
        int sadcount=0;                       // sad 카운트
        char ch[] = new char[str.length()];   // 문자열 담을 char 배열 선언

        // when
        for(int i=0;i<str.length();i++){
            ch[i]=str.charAt(i);            // ch[]에 담기

        }
        for(int i=0;i<ch.length;i++){       // 구분
            if(ch[i]==':' && ch[i+1]=='-'){
                if(ch[i+2]==')'){           // 세개다 충족하면
                    happycount++;
                }
                else if(ch[i+2]=='('){
                    sadcount++;
                }
                else{
                    continue;
                }
            }
        }
        if(happycount>sadcount){
            System.out.println("happy");
        }
        else if(happycount<sadcount){
            System.out.println("sad");
        }
        else if(happycount==sadcount){
            if(happycount==0 && sadcount ==0){
                System.out.println("none");
            }
            else {
                System.out.println("unsure");
            }
        }
        br.close();
    }
}


```


