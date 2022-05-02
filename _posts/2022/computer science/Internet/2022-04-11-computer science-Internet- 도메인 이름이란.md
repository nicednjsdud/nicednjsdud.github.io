---
title: Internet 인터넷이란?
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Computer Science
description: 인터넷이란?
tag : Internet
article_tag1: CS50
article_section: CS50
meta_keywords: CS50,computer,cs,인터넷이란?
last_modified_at: '2022-04-11 14:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

Internet 인터넷이란?
======================

## 도메인은 알았는데 도메인 이름(domain name)은 뭐지?

* 도메인이 인터넷의 주소(IP 지만 도메인 역시 주소로 생각 할 수 있으니  
  여기서는 주소라고 표현하겠습니다.) 이라면 도메인의 구성 요소에도 각자  
  이름이 정해져 있다.

```     
     https://www.google.com
     https://naver.com
     https://www.google.co.kr
```     

* 위 주소는 구글과 네이버의 주소이다. 이 주소들은 자세히 보면 dot으로 구분  
  되어져 있는것을 알 수 있다.

* google을 예시로 들어보면 www / google / com 이 모두 dot(점)으로 구분  
  되어져 있는데 이는 오른쪽부터 각각 1,2,3 단계로 구분되어 있다. 그리고  
  1단계에서 3단계로 갈수록 도메인의 범위는 작아지게 된다.

## Domain Name 3단계

* 어? 그럼 www.google.com은 3단계 도메인 이름으로 이루어져 있는건가?

```
 아니다. www.의 경우 도메인 이름에 포함되지 않는 '호스트 명'이다.
 따라서 www.google.com의 경우 총 2단계의 도메인 네임으로 이루어져 
 있음을 알 수 있다.
```

## www.google.co.kr은 뭔데?

* 이 주소도 같은 구글의 주소이다. 차이점은 com과 co.kr의 차이인데 전자의   
  경우 최상위 도메인(.com & .net & .org등)인 .com을 사용한 것이고  
  후자의 경우 국가 정책의 따른 국가 최상위 도메인을 사용한 것이다.

* 쉽게 말하면 우리나라 인터넷 환경에서 google.com으로 접속시 자동으로  
  google.co.kr로 접속되는 것이다.

```       
  - 1단계 : 국가도메인(kr)
  - 2단계 : 도메인의 성격(해당도메인이 사업체의 도메인이라는 것을 알려
                 주는 co)
  - 3단계 : 도메인 네임을 등록하는 사람이 원하는 이름
```

* 서로 다른 집이 같은 주소를 가질 수 없들이 도메인 역시 전 세계에서 유일하게  
  존재해야 하므로 도메인 네임이라는 규칙이 존재하게 된 것이고 이는 사용자가  
  임의로 변경 및 생성이 불가능하다. 
* 모든 도메인은 Root 도메인 (최상위도메인)과 이하에 역트리 구조를 가진   
  계층적 구조로 이루어져 있다.

```
  - 1단계 도메인 or Root Domain을 우리는 TLD(Top-Level Domain)이라 하고
  - 2단계 도메인을 SLD(Second-Level Domain)이라고 부른다.
   .com .net과 같은 TLD는 등록 요건을 갖춘 후 2단계에 원하는 이름을 바로 사용
   할 수도 있으며 국가 정책에따라 2,3단계를 거쳐 도메인을 설정할 수 있다.
```

출처 :  https://velog.io/@dreamjh/%EB%8F%84%EB%A9%94%EC%9D%B8-%EC%9D%B4%EB%A6%84%EC%9D%B4%EB%9E%80   
