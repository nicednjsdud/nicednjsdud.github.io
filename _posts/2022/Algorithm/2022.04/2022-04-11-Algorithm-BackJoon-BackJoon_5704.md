---
title: BackJoon Algorithm 5704
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 팬그램
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-04-11 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/5704.png)

## 풀이

* 알파벳 배열 (26칸을 만들어) 하나씩 대입 
* 만약 26개 다 0개 이상이면 Y

```java
import java.util.Scanner;

public class Back_5704 {
    public static void main(String[] args) {

        // 1. 입력
        Scanner sc = new Scanner(System.in);

       while(true){
           String str =sc.nextLine();    // 문장 입력
           int alphabet[]=new int[26];   // 알파벳 배열생성
           if(str.equals("*")){          // * 입력되면 종료
               break;
           }
           for(int i=0;i<str.length();i++){ // 각문자를 알파벳 배열에 넣기
               if(str.charAt(i) == ' '){
                   continue;
               }
               else {
                   char ch = str.charAt(i);
                   alphabet[ch - 'a']++;
               }
           }
           int count=0;               // 알파벳 갯수새기
           for(int i=0;i<26;i++){
               if(alphabet[i]!=0)     // 26개 다 들어갔는지 체크
               count++;
           }
           if(count==26){
               System.out.println("Y");
           }
           else{
               System.out.println("N");
           }
       }
    }
}

```

