---
title: BackJoon Algorithm 5054 탄산 음료
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 탄산 음료
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-04-01 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/5032.png)


## 풀이

* 첫번째 풀이 : 9개에서 3개로 한병 바꿈 그럼 6+1 =7 .. 3개로 한병 바꿈 그럼 4+1 =5
* 두번째 풀이 : 9개로 3병 바꿔서 다먹고 하나더

```java
    import java.util.Scanner;

public class Back_5032 {
    public static void main(String[] args) {
        
        Scanner sc = new Scanner(System.in);

        int have_bottle =sc.nextInt();
        int today_bottle =sc.nextInt();
        int change_bottle= sc.nextInt();
        int current_bottle=have_bottle+today_bottle;
        int count=0;
        while(current_bottle>=change_bottle){
            current_bottle-=change_bottle;
            current_bottle++;
            count++;

        }
        System.out.println(count);
        sc.close();
    }
}
```

```java
    import java.util.Scanner;

public class Back_5032_2 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int have_bottle =sc.nextInt();
        int today_bottle =sc.nextInt();
        int change_bottle= sc.nextInt();
        int count=have_bottle+today_bottle;
        int temp=0;
        boolean run= true;
        while(run){
            if(count>=change_bottle){
                count=count/change_bottle;
                temp+=count;
            }
            else {
                run=false;
            }

        }
        System.out.println(temp);
        sc.close();
    }
}

```

