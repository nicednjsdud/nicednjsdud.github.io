---
title: (Cloud) 쿠버네티스 - Desired State
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Cloud
description: Desired State
tag: Cloud
article_tag1: Cloud
article_section: computer
meta_keywords: Cloud
last_modified_at: "2022-10-31 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# Desired State

![alt](/assets/images/post/cloud/4.png)

## 1. 쿠버네티스의 다양한 기능등 사용 방법

![alt](/assets/images/post/cloud/7.png)

- 쿠버네티스는 원하는 상태를 계속 체크하여 문제가 있다면 자동으로 조치한다.
- 원하는 상태란?
  - 관리자가 바라는 환경을 의미하고, 좀 더 구체적으로는 얼마나 많은 웹서버가 구동되고 있으면 좋은지,  
    몇번 포트로 서비스하기를 원하는 등을 말한다.
- 쿠버네티스는 복잡하고 다양한 작업을 하지만 자세히 들여다보면, 현재 상태를 모니터링 하면서 관리자가  
  설정한 원하는 상태를 유지하려고 내부적으로 이런저런 작업을 하는 단순한 로직을 가지고 있다.

## 2. 원하는 상태 설정 방법

- 쿠버네티스에서는 YAML 또는 JSON 파일을 사용해, 원하는 애플리케이션 상태(Desired State)에 대해  
  명시적으로 설정할 수 있다.

### 1) ex)

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  selector:
    matchLabels:
      app: nginx
  replicas: 2 # tells deployment to run 2 pods matching the template
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
        - name: nginx
          image: nginx:1.14.2
          ports:
            - containerPort: 80
```

- 작성을 완료하고 나면, 쿠버네티스가 작성 파일에 정의된 사양에 따라 컨테이너의 라이플사이클을 관리
- 시스템으로 컨테이너 기반 애플리케이션 및 서비스의 설정, 라이프사이클, 스케일 등을 관리할수 있게 된다.

## 3. 어떠한 것들을 설정할수 있는지

- 쿠버네티스에서는 Pod를 배포할 때, 컨테이너에 필요한 각 리소스의 양을 선택적으로 지정할 수 있다.
- 일반적으로는 CPU, 메모리 그리고 다양한 것들을 제한할 수 있다.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: frontend
spec:
  containers:
    - name: app
      image: images.my-company.example/app:v4
      resources:
        requests:
          memory: "64Mi"
          cpu: "250m"
        limits:
          memory: "128Mi"
          cpu: "500m"
    - name: log-aggregator
      image: images.my-company.exammple/log-aggregator:v6
      resources:
        requests:
          memory: "64Mi"
          cpu: "250m"
        limits:
          memory: "128Mi"
          cpu: "500m"
```

- YAML 파일에 다음과 같이 컨테이너에 대한 리소스 제한(limit)을 지정하면, 설정한 제한보다  
  많은 리소스를 사용할수 없도록 해당 제한을 적용합니다.

<a href="https://tech.ktcloud.com/68?category=465864">출처 : https://tech.ktcloud.com/68?category=465864</a>
