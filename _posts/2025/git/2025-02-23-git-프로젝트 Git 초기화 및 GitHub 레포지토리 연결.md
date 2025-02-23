---
title: (Git) Ktor 프로젝트 Git 초기화 및 GitHub 레포지토리 연결
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Git
description: 프로젝트 Git 초기화 및 GitHub 레포지토리 연결
tag: git
article_tag1: git
article_section: git
meta_keywords: git,github,gitcommit
last_modified_at: "2025-02-23 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: "목차"
---

# **📌 Ktor 프로젝트 Git 초기화 및 GitHub 레포지토리 연결**

---

## **📌 1. Git 초기화 및 GitHub 레포지토리 연결**

Ktor 프로젝트를 **Git으로 관리**하고 GitHub에 **원격 저장소**를 연결하는 방법을 정리했습니다.

---

### **1️⃣ 터미널을 열고 Ktor 프로젝트 폴더로 이동**

```sh
cd /path/to/your/ktor-project
```

📌 `/path/to/your/ktor-project` 부분을 **자신의 프로젝트 경로로 변경**하세요.

---

### **2️⃣ Git 초기화 (.git 폴더 생성)**

```sh
git init
```

✅ 해당 명령어를 실행하면 `.git` 폴더가 생성되며, Git으로 프로젝트를 관리할 수 있습니다.

---

### **3️⃣ GitHub 레포지토리를 원격 저장소로 추가**

👉 **GitHub에서 만든 레포지토리 URL을 복사한 후 아래 명령어 실행**

```sh
git remote add origin https://github.com/YOUR_GITHUB_USERNAME/YOUR_REPOSITORY_NAME.git
```

📌 `YOUR_GITHUB_USERNAME` 및 `YOUR_REPOSITORY_NAME`을 **자신의 GitHub 계정과 레포지토리 이름으로 변경**하세요.

---

## **📌 2. .gitignore 파일 추가 (Gradle/Kotlin 관련 불필요한 파일 제외)**

### **1️⃣ .gitignore 파일 생성**

📌 프로젝트 폴더 내 `.gitignore` 파일을 만들고 아래 내용을 추가하세요.

```bash
### Gradle ###
.gradle/
build/
out/
.idea/
*.iml
*.log

### Environment ###
.env
```

✅ `.gitignore` 파일을 추가하지 않으면 빌드된 파일까지 올라가서 **불필요한 용량 증가**할 수 있습니다.

---

## **📌 3. 변경 사항 커밋 및 푸시**

### **1️⃣ Git 상태 확인**

```sh
git status
```

📌 현재 변경된 파일 목록을 확인할 수 있습니다.

### **2️⃣ 모든 변경 사항 추가**

```sh
git add .
```

✅ `git add .`를 사용하면 **모든 변경 사항을 스테이징**합니다.

### **3️⃣ 커밋하기**

```sh
git commit -m "Initial commit"
```

📌 `-m "Initial commit"` 부분은 **커밋 메시지**이므로, 원하는 메시지로 변경할 수 있습니다.

### **4️⃣ GitHub에 푸시**

```sh
git push -u origin main
```

✅ `main` 브랜치로 변경 사항을 푸시합니다.  
(🚨 `master` 브랜치를 사용하는 경우 `main` 대신 `master`를 입력하세요.)

---

## **📢 결론**

✅ **Git을 초기화하고 GitHub에 연결하는 과정**을 정리했습니다.  
✅ **.gitignore 파일 추가**로 불필요한 파일 업로드 방지  
✅ **변경 사항을 커밋하고 GitHub에 푸시**하여 원격 저장소와 동기화 완료 🎉

---
