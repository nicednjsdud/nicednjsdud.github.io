---
title: (컴퓨터 개론) 10-1 데이터베이스의 개념
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 데이터베이스의 개념
tag: Computer Science
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,컴퓨터 개론
last_modified_at: "2023-01-01 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 컴퓨터 개론 - 데이터베이스의 개념

## 1. 파일 처리 시스템

- 여러 개의 파일을 **통합**하고 관리, 운영 할수 있는 시스템 **(데이터베이스)**
- 자료처리

### 1) 파일 처리 시스템과 문제점

#### (1) 파일 처리 개념 (Flat File)

- 파일 : 같은 **유형**의 데이터 모음, 파일의 조직은 특정한 정보처리의 목적을 달성하기 위해 구축
- 파일 처리 시스템은 1960년대부터 사용, 각 응용 프로그램마다 별도의 파일을 조직

![alt](/assets/images/post/ComputerStudy/504.png)

#### (2) 파일 처리의 문제점

- 데이터 파일들에 **중복된** 데이터 존재, 데이터 간의 불일치
- 데이터의 공유가 부족, 새로운 프로그램 개발을 위해서는 **새롭게** 파일 구성
- 데이터의 활용이 떨어지고 응용 프로그램의 **생산성** 낮음
- 데이터 보안 미흡, **데이터 회복**의 어려움

![alt](/assets/images/post/ComputerStudy/505.png)

## 2. 데이터베이스

- 데이터베이스는 통합, 공유를 기반으로 많은 파일을 총체적으로 관리하는 방안

### 1) 데이터베이스의 개념

- 한번 구축한 데이터가 다양한 목적을 가진 여러 응용에서 중복적으로 사용, DB는 데이터의 공유에 기반
- **통합**된 데이터이며 **공유** 데이터
- 데이터의 **중복성**을 가급적 배제하여 정확성 향상

![alt](/assets/images/post/ComputerStudy/506.png)

### 2) 데이터베이스의 특성

- 임의의 질의에 대하여 원하는 정보가 **실시간으로** 검색
- 상황에 따라 동적으로 데이터 구조가 변화하고 새로운 데이터 삽입 및 데이터의 삭제하여 데이터의 **정확성** 유지
- 다수의 사용자를 위하여 **동시에** 접근 가능하여 공유 기능제공
- 원하는 데이터를 참조하는 값에 따라서 물리적 저장장치에서 **쉽게** 엑세스

### 3) 논리적(개념적) 데이터베이스 : 개체와 관계

- 데이터베이스의 논리적 구성 요소(**사용자** 관점)와 물리적 구성(**시스템** 관점) 요소
- 논리적 구성요소 : 개체(Entity), 관계(Relationship), 속성(Attribute)

![alt](/assets/images/post/ComputerStudy/507.png)
