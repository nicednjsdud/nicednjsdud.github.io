---
title: (Git) Git Bash로 GitHub에 코드 푸시하는 방법
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Git
description: Git Bash로 GitHub에 코드 푸시하는 방법
tag: git
article_tag1: git
article_section: git
meta_keywords: git,github,gitcommit
last_modified_at: "2024-09-19 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# Git Bash 로 push 하는 법

- 원격 저장소가 연결 되어있다고 가정합니다.

## 1. 깃 상태 확인

일단 먼저 git의 상태를 확인합니다.

```bash
$ git status
```

![alt](/assets/images/post/ComputerStudy/1138.png)

- 아직 스테이징 되기 전 상태입니다.

## 2. 변경된 파일 스테이징

```bash
$ git add .
```

![alt](/assets/images/post/ComputerStudy/1139.png)

### 3. 커밋

```bash
$ git commit -m "작업 내용에 대한 메시지"
```

![alt](/assets/images/post/ComputerStudy/1140.png)

### 4. 푸시

```bash
$ git push origin main
```

![alt](/assets/images/post/ComputerStudy/1141.png)

### 로그 확인

```bash
$ git log
```

![alt](/assets/images/post/ComputerStudy/1142.png)
