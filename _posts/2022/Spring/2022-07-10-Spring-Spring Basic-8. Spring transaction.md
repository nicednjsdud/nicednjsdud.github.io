---
title: (Spring) 8. 스프링 트랜잭션
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Spring
description: 스프링 트랜잭션
tag: Spring Basic
article_tag1: Spring Web
article_section: Spring Web
meta_keywords: Spring, backend ,framework
last_modified_at: "2022-07-10 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# Spring transaction

## 1. 트랜잭션(Transaction)

- 여러 개의 DML 명령문을 하나의 논리적인 작업 단위로 묶어서 관리하는 것
- ALL 또는 Nothing 방식으로 작업을 처리함으로써 작업의 일관성을 유지함.
- Web Application에서는 Service 클래스의 각 메서드가 애플리케이션의 단위 기능을 수행

![alt](/assets/images/post/spring/22.png)

## 2. Transaction의 속성 (ACID)

### 1) 원자성(Atomicity)

- 나눌 수 없는 하나의 작업으로 다뤄줘야 함

### 2) 일관성(Consistency)

- Tx 수행 전과 후가 일관된 상태를 유지해야 함

### 3) 고립성 (Isolation)

- 각 Tx는 독립적으로 수행되어야 함.

### 4) 영속성 (Durability)

- 성공한 Tx의 결과는 유지되어야 함.

## 3. 웹 에플리케이션에서 묶어서 처리하는 단위 기능 예

- 게시판 글 조회 시 해당 글을 조회하는 기능과 조회 수를 갱신하는 기능
- 쇼핑몰에서 상품 주문 시 주문 상품을 테이블에 등록하는 기능과 주문자의  
  포인트를 갱신하는 기능
- 은행에서 송금 시 송금자의 잔고를 갱신하는 기능과 수신자의 잔고를 갱신하는 기능

  - 출금과 입금이 모두 성공하지 않으면 실패
  - 두 계좌 잔고의 갱신이 모두 정상적으로 이루어지면 최종적으로 반영(commit)함

    - 작업 내용을 DB에 영구적으로 저장

  - 중간에 이상이 발생할 경우 이전의 모든 작업 취소, 즉 롤백(rollback) 시킴
    - 마지막 커밋으로 복귀 (최근 변경사항을 취소)

## 4. Spring transaction 속성

### 1) propagation

#### 1.1 트랜잭션 전파 규칙 설정

- REQUIRED

  - 트랜잭션 필요
  - 진행 중인 트랜잭션이 있는 경우 해당 트랜잭션 사용
  - 트랜잭션이 없으면 새로운 트랜잭션 생성 **(default)**

- REQUIRED_NEW
  - Tx이 진행 중이건 아니건, 새로 Tx 시작

### 2) isolation

### 3) readOnly

### 4) rollbackFor

### 5) noRollbackFor

### 6) time
