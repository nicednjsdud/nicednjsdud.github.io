---
title: (컴퓨터 개론) 11-3 사물 인터넷 기술의 활용
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 사물 인터넷 기술의 활용
tag: Computer Science
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,컴퓨터 개론
last_modified_at: "2023-01-10 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 컴퓨터 개론 - 사물 인터넷 기술의 활용

## 1. 사물 인터넷 활용 분야

- 농업, 유통, 산업 등 자동차 기술의 대부분은 사물 인터넷을 기반으로 만들어진 것

### 1) 5G 시대

#### (1) 다양한 스마트 서버 시대를 연 4G LTE

- 4G LTE(Long Term Evolution)
- 고속으로 실시간 동영상 스트리밍 서비스를 시작하여 서비스의 다양화 - LTE-A(어드밴스)와 광대역 LTE는 LTE보다 2배 고속
- 주파수 3개를 묶어 6개 고속인 LTE도 출시

#### (2) 세계 최초 LTE-A 지원 스마트폰 갤럭시S4

![alt](/assets/images/post/ComputerStudy/615.png)

#### (3) LTE보다 1000배 빠른 고속인 5G

- 3G보다 1000배 빠른 빛의 인터넷, 초당 Gb의 데이터 전송 800Mb의 다운로드 시 LTE는 3분,  
  LTE-A는 40초, 5G 이동통신은 1초
- 5G는 4G까지 사용했던 저대역 주파수를 고대역 주파수를 확보해서 속도를 높인 것

![alt](/assets/images/post/ComputerStudy/616.png)

- 5G 기반으로 초고화질(UHD), 홀로그램, 모바일 입체영상 등 다양한 서비스가 일반화되면 IoT 시대가 도래
- 무인자동차 시대, 자동냉장고, 자동실내전등 등 새로운 생활 패러다임 전개

![alt](/assets/images/post/ComputerStudy/617.png)

### 2) 사물 인터넷의 활용 분야

#### (1) 개인 영역

- 스마트 홈, 헬스 케어, 웨어러블 기기, 무인자동차

#### (2) 제조업 및 비즈니스 영역

- ICT 기술을 융합하여 새로운 산업

#### (3) 도시와 같은 인프라 영역

- 도시 보안, 위기관리, 에너지 관리 등

![alt](/assets/images/post/ComputerStudy/618.png)

#### (4) 구글 글래스

- 오른쪽 시야에 있는 프리즘을 통해 시야 정보를 디스플레이하여 증강현실 서비스를 제공하는 기기
- 문자 입력 대신에 음성, 모션, 안구 이동 등의 새로운 인터페이스

![alt](/assets/images/post/ComputerStudy/619.png)

- 사진, 동영상 활용
- 스마트폰 활용

#### (5) 갤럭시 기어 or 애플 워치

- 스마트폰과 연동을 통해서 통화, 메시지 확인, 사진 촬영 등 스마트폰 기능을 확장한 것
- 운동관리 기능도 포함

#### (6) 가전 기기

- 클라우드 기반의 스마트 홈서버를 중심으로 에어컨, 냉장고, 청소기, 가스 등을 원격으로 제어하는 시스템
- 스마트폰으로 제어

![alt](/assets/images/post/ComputerStudy/620.png)

#### (7) LG전자 홈챗

- 홈 챗은 모바일 메신저 ‘라인’을 기반으로 채팅형식으로 가전제품과 일상단어로 정보를 주고 받는 LG 시스템
- 모바일 메신저 창에 외출, 귀가, 파티, 취침 등 입력하여 상황에 맞게 작동(연결과 소통)

![alt](/assets/images/post/ComputerStudy/621.png)

## 2. 산업 인터넷과 인더스트리 4.0

- 기계 학습을 통한 제조 공정의 혁신으로 지능화된 기계, 고도화된 분석, 항상 연결되는 작업환경으로  
  스마트한 제품 생산 개발하는 시스템

### 1) 산업 인터넷의 부상

- GE사는 제품에 센서를 부착해서 관련 데이터를 수집·분석함으로 생산성과 효율성을 높이고 있으며, 이를 산업 인터넷으로 명명

#### (1) 제1의 물결 산업혁명

- 기계와 공장에 산업의 기반

#### (2) 제2의 물결 인터넷 혁명

- 정보와 네트워크로 분배되어 전문화, 자동화, 기계 학습으로 스마트 커넥티브 제품생산과 그에 대한 서비스

#### (3) 제3의 물결 산업 인터넷

- 기계 학습을 통한 제조공정의 혁신으로 지능화된 기계, 고도화된 분석, 항상 연결되는 작업자로  
  스마트한 제품생산·개발(소프트웨어 기업 기반으로)

#### (4) 산업 인터넷의 구성(출처: GE코리아)

![alt](/assets/images/post/ComputerStudy/622.png)

### 2) 인더스트리 4.0

- IoT 활용 분야 중 가장 큰 부분을 제조업과 헬스케어가 차지
  - 향후 10년간 제조업 분야 14.4조 달러 (전체 IoT 분야의 27%)
  - 기존 제조 산업에 IoT 기술 융합, 다품종 소량생산
- GE사는 산업 인터넷(Industrial Internet) 명명 3 독일에서는 인더스트리 4.0(2011)
  - 스마트 공장개념으로 제 4차 산업혁명을 주장

#### (1) 인더스트리 4.0의 발전 과정

![alt](/assets/images/post/ComputerStudy/623.png)

### 3) 웨어러블 컴퓨터의 활용

#### (1) 센서가 부착된 웨어러블 기기를 통하여 상황을 인식하고 측정

- 임의의 장소 및 시간, 빅데이터 활용
- 항상 켜져 있는 상태(Always-On), 사용자의 주변 환경을 인식(Environment-Aware),  
  항상 연결되어(Connected) 실시간 정보교환 가능
- 웨어러블 컴퓨터의 특성 (유형 : 액세서리형, 의류일체형, 신체부착형, 생체인식형)

![alt](/assets/images/post/ComputerStudy/624.png)
