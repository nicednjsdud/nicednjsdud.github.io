---
title: CS50 1-7강 image
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Computer Science
description: image
tag : CS50
article_tag1: CS50
article_section: CS50
meta_keywords: CS50,computer,cs,image
last_modified_at: '2022-04-18 14:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

![alt](/assets/images/post/computer science/CS50/1/0.jpg)


이미지
======

## 이미지

* 이미지는 여러 가지 파일 유형으로 저장된다.
* 보통 우리가 많이 볼수 있는 **이미지 파일 형식**으로 비트맵(.bmp), JPG(.jpg)  
  PNG(.png)등이 있다.
* 각각의 파일 유형들에는 장점과 단점이 있다. 
* 어떤 파일 유형으로 저장하는가에 따라 이미지 파일이 더크거나 작을 수 있고,  
  더 선명하거나 그렇지 않을 수 있다.

## 사진 파일에 들어있는 정보

* 사진을 찍어 이미지에 저장하면 그이미지는 보통 **JPEG**라는 확장자를 갖게되고  
  이미지를 압축하여 저장한다.
* 윈도우에서 많이 볼 수 있는 파일 형식에는 BMP가 있다.
* 하나의 이미지를 다양한 이미지 파일 형식으로 저장할 수 있는데, 저장되는 형식  
  에 따라 파일 안에 들어가 있는 비트 데이터들의 구조 또한 다르다.
* 각각의 이미지 파일은 보통 첫 부분에 파일을 구분할 수 있는 구분자를 넣는다.
* JPEG의 첫 부분에는 16진수 단원에서 배웠던 255 216 255 라는 10진수로 시작
* JPEG파일을 들여다보면 파일을 구분할 수 있는 정보가 처음에 보이고 나머지  
  정보들이 그 다음에 저장되게 된다.

## 비트맵 이미지 파일에 들어있는 정보

* BMP 파일 형식은 이미지 데이터를 가장 단순하게 저장한다.
* 대신 압축을 하지않아 파일크기가 크다는 단점이있다.
* JPEG 파일처럼 파일의 가장 처음 부분에 비트맵 파일에 대한 정보가 있다.

![alt](/assets/images/post/computer science/CS50/1/7.png)

