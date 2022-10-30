---
title: (AWS) EC2란?
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - AWS
description: EC2란?
tag: Cloud
article_tag1: Cloud
article_section: computer
meta_keywords: Cloud
last_modified_at: "2022-10-29 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# Amazon EC2 란?

## 1. Amazon Elastic Compute Cloud (Amazon EC2)

- 아마존 웹 서비스(AWS)의 여러 서비스 중 가장 먼저 생겨난 서비스 중 하나이다.
- 가장 범용적으로 사용한다.
- EC2는 독립된 컴퓨터 한대를 임대해서 사용할 수 있게해주는 서비스다.
- 단시간안에 여러 가지 프로세서, 스토리지, 네트워킹, 운영체제, 구매모델을 선택하여 생성

## 2. EC2의 장점

- 마우스 클릭 몇번만으로 컴퓨터 한대를 구성
- 원하는 스펙의 가상 서버를 구축, 스펙을 사용할만큼의 비용만 지불
- 스펙을 줄이거나 높이는게 가능
- EBS (Elastic Block Store) 불륨을 구성하여 영구 스토리지로 저장이 가능
- EIP (Elastic IP Address)를 사용하여 고정 IP할당 가능

## 3. EC2리전 이란?

- AWS는 나라(리전) 별로 데이터 센터를 가지고 있다.
  - 참고 : 모든 나라마다 가지고 있지는 X
- 데이터 센터는 컴퓨터들이 모여있는 공간이다.

## 4. EC2 Instance

- 하나의 EC2 Instance는 컴퓨터 한대를 의미
  - Instance 다섯개를 사용중이다는 컴퓨터 5개를 사용중을 의미

## 5. 요금

### 1) 온디맨드

- 선결제 금액이나 장기 약정 없이 저렴하고 유연하게 Amazon EC2를 사용하기 원하는 사용자
- 단기의 갑작스럽거나 예측할 수 없는 워크로드가 있으며, 중단되어서는 안되는 애플리케이션
- Amazon EC2에서 처음으로 개발 또는 시험 중인 애플리케이션

### 2) 스팟 인스턴스

- 시작 및 종료 시간이 자유로운 애플리케이션
- 컴퓨팅 가격이 매우 저렴해야만 수익이 나는 애플리케이션
- 대량의 서버 용량 추가로 긴급히 컴퓨팅 파워가 필요한 사용자

### 3) Saving Plans

- 1년 또는 3년 기간의 일정 사용량 약정을 조건으로 EC2 및 Fargate 사용량에 대해 저렴한 요금을  
  제공하는 유연한 요금

### 4) 예약 인스턴스

- 수요가 꾸준한 애플리케이션
- 예약 용량이 필요할 수 있는 애플리케이션
- 총 컴퓨팅 비용을 절감하기 위해 1년 또는 3년 동안 EC2를 사용하기로 약정할 수 있는 고객

### 5) 전용 호스팅

- EC2에서 Microsoft 및 Oracle 같은 공급업체의 적격 소프트웨어 라이선스를 사용할 경우
- 기존의 물리적 서버에서 EC2를 사용할 경우
- 온디맨드로 구매 가능(시간당).
- 온디맨드 요금과 비교하여 최대 70% 할인된 예약 인스턴스로 구매 가능

### 6) 초당 결제

- 온디맨드, 예약 및 스팟 형태
- 모든 리전 및 가용 영역
- Amazon Linux 및 Ubuntu
