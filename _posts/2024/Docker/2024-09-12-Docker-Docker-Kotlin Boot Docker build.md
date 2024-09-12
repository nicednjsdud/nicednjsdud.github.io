---
title: (Docker) Docker로 Kotlin Spring 프로젝트 빌드 및 이미지화
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Docker
description: Docker
tag: Docker
article_tag1: Docker
article_section: Docker
meta_keywords: Docker
last_modified_at: "2024-09-12 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# Docker로 Kotlin Spring 프로젝트 빌드 및 이미지화

- 회사에서 Kafka를 쓸일이 있어 사내 IP로 연결을 해보려했지만,  
  보안이슈 등으로 이벤트가 오지않아 한 PC에서 모든 서버를 Docker에 올려 테스트하기로 했다.

## 목차

1. Dockerfile 작성
2. Docker 이미지 빌드
3. Docker 이미지 실행

## 1. Dockerfile 작성

```Dockerfile
# 1. Gradle 기반의 Kotlin 프로젝트 빌드를 위한 이미지 설정
FROM gradle:7.5.1-jdk17 as builder
WORKDIR /home/gradle/src

# 2. 프로젝트 소스 파일을 컨테이너에 복사
COPY --chown=gradle:gradle . /home/gradle/src
USER root
RUN chown -R gradle /home/gradle/src

# 3. Gradle 빌드 실행
USER gradle
RUN gradle clean build

# 4. 최종 실행용 이미지를 생성
FROM openjdk:17-alpine
CMD mkdir /app

# 5. 빌드된 JAR 파일을 복사
COPY --from=builder /home/gradle/src/build/libs/*.jar /app/

# 6. 애플리케이션 실행
WORKDIR /app
CMD ["java", "-jar", "my-app-0.0.1-SNAPSHOT.jar"]

# my-app-0.0.1-SNAPSHOT은 빌드된 JAR파일 이름을 넣으면됨
# 예) test-app-for-docker-0.0.01-SNAPSHOT.jar
```

## 설명

```dockerfile
FROM gradle:7.5.1-jdk17 as builder
```

- Gradle 7.5.1과 JDK 17이 포함된 이미지를 사용하여 빌드 환경을 구성

```dockerfile
WORKDIR /home/gradle/src
```

- 컨테이너 내에서 작업할 디렉토리를 설정

```dockerfile
COPY --chown=gradle:gradle . /home/gradle/src
```

- 현재 디렉토리의 모든 파일을 /home/gradle/src로 복사, 소유자를 gradle 사용자로 설정

```dockerfile
USER root
```

- root 사용자로 변경하여 소유권 변경 작업을 수행

```dockerfile
RUN chown -R gradle /home/gradle/src
```

- /home/gradle/src 디렉토리 및 하위 파일들의 소유자를 gradle로 변경

```dockerfile
USER gradle
```

- gradle 사용자로 변경

```dockerfile
RUN gradle clean build
```

- 프로젝트를 빌드

```dockerfile
FROM openjdk:17
```

- 빌드한 결과물을 실행하기 위한 가벼운 OpenJDK 17 이미지를 사용

```dockerfile
CMD mkdir /app
```

- /app 디렉토리를 생성 (JAR 파일을 복사할 목적)

```dockerfile
COPY --from=builder /home/gradle/src/build/libs/\*.jar /app/
```

- 빌드한 JAR 파일을 /app 디렉토리로 복사

```dockerfile
WORKDIR /app
```

- 컨테이너 내에서 /app 디렉토리를 작업 디렉토리로 설정

```dockerfile
CMD ["java", "-jar", "my-app.jar"]
```

- JAR 파일을 실행

## 2. Docker 이미지 빌드

```bash
docker build -t my-spring-app .
```

- 위 명령어는 Dockerfile을 기반으로 my-spring-app이라는 이름으로 이미지를 빌드합니다.

![alt](/assets/images/post/ComputerStudy/1138.png)

## 3. Docker 이미지 실행

```bash
docker run -d -p 8080:8080 my-spring-app
```

- 이 명령어는 애플리케이션을 백그라운드에서 실행하며, 로컬 컴퓨터의 8080 포트로 연결됩니다.

- Docker desktop 으로 확인할 수 있습니다.

![alt](/assets/images/post/ComputerStudy/1139.png)
