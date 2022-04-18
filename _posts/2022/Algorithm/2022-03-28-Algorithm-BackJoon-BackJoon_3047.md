---
title: BackJoon Algorithm 3047 ABC
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: ABC
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

![alt](/assets/images/post/Algorithm/3047.png)



## 풀이

* bubbel sort 알고리즘과 비슷하게 문제 풀이

```java
import java.util.Arrays;
import java.util.Scanner;

public class Back_3047 {
    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);
        int num[]=new int [3];

        int temp=0;

        for(int i=0;i<3;i++) {
            num[i]=sc.nextInt();
        }

        Arrays.sort(num);
        String str=sc.next();
            if(str.charAt(0)=='A'){
                if(str.charAt(1)=='B'){
                    Arrays.sort(num);              // 1.2.3
                }
                else if(str.charAt(1)=='C'){       // 1.3.2
                    temp=num[1];
                    num[1]=num[2];
                    num[2]=temp;
                }
            }
            else if(str.charAt(0)=='B'){            // 2.1.3
                if(str.charAt(1)=='A'){
                    temp=num[1];
                    num[1]=num[0];
                    num[0]=temp;
                }
                else if(str.charAt(1)=='C'){        // 2.3.1
                    temp=num[0];
                    num[0]=num[1];
                    num[1]=num[2];
                    num[2]=temp;
                }
            }
            else if(str.charAt(0)=='C'){
                if(str.charAt(1)=='A'){             // 3.1,2
                    temp=num[0];
                    num[0]=num[2];
                    num[2]=num[1];
                    num[1]=temp;
                }
                else if(str.charAt(1)=='B'){        // 3.2.1
                    temp=num[0];
                    num[0]=num[2];
                    num[2]=temp;
                }
            }
        for(int i=0;i<3;i++){
            System.out.print(num[i]+" ");
        }


    }
}

```

