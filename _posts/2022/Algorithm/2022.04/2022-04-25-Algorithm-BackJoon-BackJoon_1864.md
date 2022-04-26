---
title: BackJoon Algorithm 1864 문어숫자
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Algorithm
description: 문어숫자
tag : BackJoon
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: BackJoon,Algorithm, java
last_modified_at: '2022-04-25 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

BackJoon Algorithm - Java
====================

![alt](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

## 문제

![alt](/assets/images/post/Algorithm/1864_1.png)
![alt](/assets/images/post/Algorithm/1864_2.png)



## 풀이

* BufferedReader 클래스를 사용해 보았다.
* pow(double a, double b) 함수를 이용해서 8진수를 10진수로 변환한다.
    * 첫번째인자는 밑수이고, 두번째 인자는 지수입니다.

```java

import java.io.BufferedReader;
import java.io.InputStreamReader;

public class Back_1864{
    public static void main(String[] args) throws Exception{

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int count=0;
        int sum=0;
        while(true){

            String str = br.readLine();
            if(str.equals("#")){        // 입력 #이 들어오면 종료
                break;
            }
            for(int i=0;i<str.length();i++){
                int temp=0;             // 기호를 숫자로 바꿔주기
                switch(str.charAt(i)) {
                    case '-':
                        temp = 0;
                        break;
                    case '\\':
                        temp = 1;
                        break;
                    case '(':
                        temp = 2;
                        break;
                    case '@':
                        temp = 3;
                        break;
                    case '?':
                        temp = 4;
                        break;
                    case '>':
                        temp = 5;
                        break;
                    case '&':
                        temp = 6;
                        break;
                    case '%':
                        temp = 7;
                        break;
                    case '/':
                        temp = -1;
                }
                sum +=temp*Math.pow(8,str.length()-1-count);// 8진수를 10진수로 변환
                count++;
            }
            System.out.println(sum);
            count=0;
            sum=0;
        }
        br.close();
    }

}
```


