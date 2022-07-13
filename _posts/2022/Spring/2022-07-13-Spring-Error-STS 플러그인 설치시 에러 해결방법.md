---
title: (Eclipse) STS 플러그인 설치시 에러 해결방법
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Spring
description: Error
tag: Error
article_tag1: Spring Basic
article_section: Spring Basic
meta_keywords: Spring, backend ,frame work
last_modified_at: "2022-07-13 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# STS 플러그인 설치시 에러 해결방법

STS Eclipse Market에서 Properties Editor가 검색이 안되서 수동 설치를 진행해봤다.

수동 URL

```
http://propedit.sourceforge.jp/eclipse/updates/
```

하지만.. 설치진행중에 요상한 에러메세지가 자꾸나오고 인스톨이 되지않았다.

```java
An error occurred while collecting items to be installed

session context was:(profile=profile, phase=org.eclipse.equinox.internal.p2.engine.phases.Collect, operand=, action=).

No repository found containing: osgi.bundle,com.android.ide.eclipse.base,21.1.0.v201302060044-569685

No repository found containing: osgi.bundle,com.android.ide.eclipse.ddms,21.1.0.v201302060044-569685

No repository found containing: org.eclipse.update.feature,com.android.ide.eclipse.ddms,21.1.0.v201302060044-569685
```

삽질을 열심히하다가 구글링을 해보니..

플러그인 설치 창에서 "Contact all update sites during install to find required software" 항목을 해체하면 설치가된다해서
다시 설치해봤다.

![alt](/assets/images/post/spring/33.png)

해결 완료..
