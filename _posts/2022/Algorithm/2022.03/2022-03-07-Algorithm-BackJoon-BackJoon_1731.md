---
title: BackJoon Algorithm 1731 추론
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 추론
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-03-07 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.PNG)

## 문제

![alt](/assets/images/post/Algorithm/1731.png)




## 풀이

* 등차 수열의 경우 세 항 중 근접한 항 끼리 차이를 알아내고 차이가 똑같다면  
  이를 등차 수열(AP)로 판단한다. 판단이 되었다면 다시 다음 항은 마지막 항과 차이   
  값을 더해주면 된다.
* 이후 등비 수열로 판단한다. 이후 마지막 항에 공비를 곱해주면 된다.


```java
import java.util.Scanner;

public class Back_1731 {
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int count = sc.nextInt();
        int arr[]=new int[count];
        int n=0;
            for(int i=0;i<count;i++){
                arr[i]=sc.nextInt();
            }
        for(int i=0;i<arr.length;i++) {

            if ((arr[i + 1] - arr[i]) == (arr[arr.length-1] - arr[arr.length - 2])) {
                //등차수열
                n = arr[arr.length-1] + (arr[i+1] - arr[i]);
                break;
            } else {
                //등비수열
                n = arr[arr.length-1] * (arr[i+1] / arr[i]);
                break;
            }
        }
        System.out.println(n);
        sc.close();



    }
}

```


