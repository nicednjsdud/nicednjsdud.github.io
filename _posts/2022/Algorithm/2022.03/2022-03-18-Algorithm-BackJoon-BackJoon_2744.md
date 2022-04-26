---
title: BackJoon Algorithm 2744 대소문자 바꾸기
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 대소문자 바꾸기
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-03-18 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/2744.png)



## 풀이

* char형으로받아 아스키코드값으로 구분하여 + 32 or - 32로 변환

```java
    import java.util.Scanner;

public class Back_2744 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        //given
        String str=sc.nextLine();
        char arr[] = new char[str.length()];
        //when
        for(int i=0;i<str.length();i++){
            if(65<=str.charAt(i) && str.charAt(i)<=90){
                arr[i]=(char)(str.charAt(i)+32);

            }
            else if(97<=str.charAt(i) && str.charAt(i)<=122){
                arr[i]=(char)(str.charAt(i)-32);

            }
        }
        //then
        System.out.println(arr);


    }
}
```


