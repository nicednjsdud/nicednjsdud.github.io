---
title: (시스템 프로그래밍) 14-2 디바이스 드라이버 구성 (문자 디바이스 드라이버)
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

# 시스템 프로그래밍 - 디바이스 드라이버 구성 (문자 디바이스 드라이버)

## 1. 문자 디바이스 드라이버

### 1) file 구조체

- **디바이스 드라이버 구현시 사용**
- c 라이브러리에 정의된 FILE과는 다름
- 응용 프로그램에서는 사용할 수 없고, 단지 **커널**에서만 사용
- **파일 연산을 위한 인자 전달 방법으로 사용**

```c
  struct file{

    structdentryf_dentry;         // 파일에 대한 디렉토리 엔트리
    structsmount *f_vfsmnt;
    structfile_operationsf_op;    // 다양한 파일 연산 함수가 정의된 파일 연산 구조체를 지시
    atomic_tf_count;              // 프로세스 파일 참조 횟수
    unsigned intf_flags;          // 접근모드, 비블록킹, 생성, 첨부 등에 관련된 플래그
    mode_t f_mode;                // 파일 모드로 FMODE_READ or FMODE_WRITR 구분
    loff_t f_pos;                 // 현재 읽기/쓰기 위치
    unsigned long f_reada, f_ramax, f_raend, f_ralen, f_rawin;
    structfown_structf_owner;
    unsigned intf_uid, f_gid;     // 파일 사용자 및 그룹 식별자
    intf_error;
    unsigned long f_version;
    void *private_date;           // 시스템 호출간에 필요한 정보를 보존하기 위해 사용
  };
```

### 2) 파일 연산 구조체

- 파일 연산 구조체 변수를 커널에 등록하는 것이 디바이스 드라이버를 등록하는 것

```c
  <linux> /include/linux/fs.h에 선언
```

#### (1) 응용 프로그램

- 저수준 파일 입출력 함수를 사용하여 디바이스 파일에 접근

#### (2) 커널

- 등록된 디바이스 드라이버의 파일 연산 구조체를 참고해 응용프로그램의 요청에 대응하는 함수 호출

```c
  structfile_operations {

    struct module *owner              // 파일 작업의 소유자, 보통 THIS_MODULE로 지정
    loff_t (*lseek)(struct file*, loff_t, int)  // 파일에서 현재 읽고 쓰는 위치 이동
    ssize_t (*read) (struct file*, char*, size_t, loff_t *) // 디바이스에서 파일 읽음
    ssize_t (*write)(struct file*, const char*, size_t, loff_t *)// 디바이스에 데이터 씀
    int (*readdir) (struct file*, void*, filldir_t);  // 디렉토리에서만 사용 함수
    unsigned int(*poll)(struct file*, structpoll_talbe_struct *);
                                                      // 현 프로세스를 대기 큐에 넣음
    int(*ioctl)(structinode*, struct file*, unsigned int, unsigned long);
                                          // 디바이스에 종속적인 명령을 만듬. 사용자가 임의로 함수 만듦
    int(*mmap)(struct file*, structvm_area_struct *)
                                          // 디바이스의 메모리를 프로세스의 메모리로 매핑
    int(*open)(structinode *, struct file *)  // 디바이스를 개방
    int(*release)(structinode *, struct file *) // 디바이스를 종료
    int(*fsync)(struct file *, structdentry *);
                             // 디바이스를 플러시함, 데이터 중에서 디바이스에 있는 것은 모두 디바이스에 씀
    int (*fasync)(int, struct file*, int);  // FASYNC 플래그 변화에 있는 디바이스 확인용
    int(*check_media_change)(kdev_t dev); // 미디어가 변경될 수 있는 블록디바이스 사용
    int (*revalidate)(kdev_t dev);    // 제거가능한 블록 디바이스에서 버퍼 캐시 관리용
    int(*lock)(strict file*, int, structfile_lock *); // 파일에 잠금 가능
  }
```
