---
title: (시스템 프로그래밍) 14-2 디바이스 드라이버 구성 (전형적인 문자 디바이스 드라이버)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 디바이스 드라이버 개념
layout: single
tag: Internet
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,시스템 프로그래밍
last_modified_at: "2023-01-28 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 시스템 프로그래밍 - 디바이스 드라이버 구성 (전형적인 문자 디바이스 드라이버)

## 1. 전형적인 문자 디바이스 드라이버

- 문자 디바이스 드라이버의 파일 연산 구조체 사용
- 파일 연산 구조체에서 필요한 필드만 선언하면 됨 (선언하지 않은 필드는 null 처리)

#### (1) 전형적인 파일 연산 구조체의 선언내용

- xxx는 일반적으로 디바이스의 이름

```c
  struct file_operations xxx_fops = {
      .owner = THIS_MODULE,
      .open = xxx_open,
      .release = xxx_release,
      .read = xxx_read,
      .write = xxx.write,
      .ioctl = xxx.ioctl,
  }
```

### 1) 디바이스 드라이버의 등록과 해제

#### (1) 문자 디바이스의 등록과 해제

```c
  intregister_chrdev(unsigned int major, const char *name, structfile_operations *fops)
  intunregister_chrdev(unsigned int major, const char *name)
```

- major : 주번호로, 0이면 사용하지 않은 주번호 중에서 동적으로 할당
- name : 디바이스의 이름으로 `/proc/devices`에 나타나 있음
- 성공 : 0이거나 양수
- 실패 : 음수

#### (2) 블록 디바이스의 등록과 해제

```c
  intregister_blkdev(unsigned int major, const char *name)
  intunregister_blkdev(unsigned int major, const char *name)
```

- major : 주번호로, 0이면 사용하지 않은 주번호 중에서 동적으로 할당
- name : 블록 디바이스 장치 이름
- 성공 : 0이거나 양수
- 실패 : 음수

#### (3) 네트워크 디바이스의 등록과 해제

```c
  intregister_netdeiv(structnet_device *dev)
  void unregister_netdev(structnet_device *dev)
```

- dev : net_device 구조체 이름
- 성공 : 0
- 실패 : 0이아닌 다른 값

#### (4) 문자 디바이스 드라이버의 등록 과정

- 커널 내부의 `chrdevs[]`배열 구조체에 적재될 디아비스 파일의 주번호가 할당되어야 함

```c
  struct char_device_struct chrdevs[MAX_PROBE_HASH];
```

1. 쉘 모드에서 `insmod foo.ko` 실행
2. `insmod` 명령어는 디바이스 드라이버 파일의 `module_init()`호출
3. `register_chrdev()`함수 실행, 주번호를 `chrdevs[]`배열의 인덱스로 사용해 배열에 접근

- 커널 내부에 `chrdevs[]`배열 구조체에 등록

4. `foo_fops`는 모듈내에 파일 연산 가리킴.

- 디바이스 드라이버에 대응하는 함수와 연관

![alt](/assets/images/post/ComputerStudy/808.png)
