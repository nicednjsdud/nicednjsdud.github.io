---
title: 1.Database 
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Database
description: 데이터베이스
tag : Database
article_tag1: Algorithm
article_section: Algorithm
meta_keywords: Database, MySQL, Oracle
last_modified_at: '2022-04-18 13:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

Database
============

## 데이터베이스 정의

* 특정 조직의 여러 사용자가 공유하여 사용할 수 있도록   
  통합해서 저장한 운영 데이터 집합

## 데이터베이스 사용 이전

### 일반적인 텍스트 파일 형태로 저장 및 관리 되었음.

* 파일 형태는 여러 사용자가 동시에 공유하기가 어려움.
* 파일의 데이터의 유실 가능성이 항상 존재하였음.

### 파일 시스템을 사용시 문제점

* 데이터 중복성 문제
* 업데이트 시 **일관성(consistency)** 유지 어려움
* **데이터 무결성(Data Integrity Constraints)** 유지 어려움
* 데이터 종속성

```
    - 파일 구조가 바뀔때마다 응용프로그램 교체 필요
```

* **동시성(Concurrrency)** 제공이 어려움
* **원자성(atomicity)** 제공 어려움

```
    - 파일 변경 중에 시스템 장애가 발생 했을 떄 처리 어려움
```

* 보안(Security) 제공 이슈

```
    - 데이터 읽기 권한 제어 
```

## 모든 것이 데이터베이스로 관리되는 시대

* 은행

```
    - 계좌정보, 입출금 내역 등
```

* 항공사 

```
    - 예약정보, 비행기 스캐줄
```

* 대학교

```
    - 학생정보, 수강신청
```

* 온라인 쇼핑몰

```
    - 고객기록, 주문 내역
```

* 제조업

```
    - 제품목록, 주문, 재고, 공급망
```

* 회사

```
    - 직원정보, 연봉
```

## 데이터베이스 특징

### 1. 실시간 접근 가능

* 목록 조회 

### 2. 계속적으로 변화

* 구입정보, 물건재고 정보

### 3. 동시 공유가 가능

* 많은 고객이 동시접속, 구매가능

### 4. 저장된 주소가 아닌 내용으로 참조 가능

* 가장 많이 팔린 제품은? 

## 데이터의 유형

### 정형 데이터 

* structured data
* **엑셀의 스프레드시트, 관계데이터베이스의 테이블**

### 반정형 데이터  

* semi-structured data
* **HTML, XML, JSON**

### 비정형 데이터

* unstructured data
* 정해진 구조가 없이 저장된 데이터
* **text, 멀티미디어 데이터**

