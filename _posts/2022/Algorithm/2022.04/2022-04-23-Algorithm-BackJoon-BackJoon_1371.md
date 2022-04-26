---
title: BackJoon Algorithm 1371 가장 많은 글자
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 가장 많은 글자
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-04-23 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/1371.png)



## 풀이

* 배열로 소문자를 담는다.
* hasNextLine() 메서드로 글자의 끝까지 입력받는다.

```java


import java.util.Scanner;

public class Back_1371 {
    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);
        int Alphabet[]=new int[26];             // 알파벳 갯수
        int max = 0;                            // 가장 많이 나온수
        while (sc.hasNextLine()) {
                 String str = sc.nextLine();
                 for (int i = 0; i < str.length(); i++) {
                    if (str.charAt(i) >= 'a' && str.charAt(i) <= 'z') {
                    Alphabet[str.charAt(i) - 'a']++;    
                    // 26개의 배열에 각 알파벳 소문자 담기
                }
            }
        }
        for(int i=0;i<26;i++){
            if(Alphabet[i]>max){
                max=Alphabet[i];                // 가장 많이 나온수 찾기
            }
        }
        for(int i=0;i<26;i++){
            if(Alphabet[i]==max){
                System.out.print((char)(i+'a'));// 똑같이 나온수 찾기
            }
        }
        sc.close();
    }
}
```


