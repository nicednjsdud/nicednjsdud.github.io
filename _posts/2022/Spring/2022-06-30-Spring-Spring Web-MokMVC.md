---
title: (Web) Mok MVC
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Spring
description: Mok MVC
tag: Spring Web
article_tag1: Spring Web
article_section: Spring Web
meta_keywords: Spring, backend ,framework
last_modified_at: "2022-06-30 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# MokMVC

## 1. MockMVC란?

- 우리는 웹 애플리케이션을 작성한 후 , 해당 웹 어플리케이션을 Tomcat이라는  
  이름의 WAS(Web Application Server)에 배포(deploy)하여 실행한다.
- 브라우저의 요청은 WAS에게 전달되는 것이고 응답도 WAS에게서 받게 된다.
- WAS는 요청을 받은 후, 해당요청을 처리하는 웹 어플리케이션을 실행한다.

```
    즉, Web API를 테스트한다는 것은 WAS를 실행해야만 된다는 문제가있다.
```

- 이런 문제를 MockMVC를 이용해 같은 역할을 수행할 수 있다.

```
    WAS 는 실행시 상당한 많은 작업을 수행한다.
    MockMVC는 웹 어플리케이션을 실행하기 위한 최소한의 기능만을 가지고 있다.
```

![alt](https://cphinf.pstatic.net/mooc/20200305_148/1583391388280d6dWl_PNG/mceclip0.png)

## 2. MockMVC Test

- 이전에 만든 방명록으로 테스트 해보겠습니다.

![alt](https://cphinf.pstatic.net/mooc/20200305_99/1583391419153fciVU_PNG/mceclip1.png)

- GuestbookApiController를 단위 테스트한다는 것은, GuestbookApiController  
  가 사용하는 GuestbookService에 대한 부분은 함께 테스트하지 않는다는것을 의미

- 이를위해 GuestbookService에 대한 목(Mock)객체를 사용할 것이고 Mokito를  
  이용해 목객체를 생성한다.

- 컨트롤러를 테스트하기 위해 MockMvc를 사용하도록 한다.

### 1) pom.xml에 mock 라이브러리 추가

```xml
<!-- test mock을 위한 라이브러리를 추가합니다. -->
        <dependency>
            <groupId>org.mockito</groupId>
            <artifactId>mockito-core</artifactId>
            <version>1.9.5</version>
            <scope>test</scope>
        </dependency>
```

### 2) GuestbookApiController.java

```java
package kr.or.connect.guestbook.controller;

import static org.mockito.Mockito.verify;
import static org.mockito.Mockito.when;
import static org.springframework.test.web.servlet.result.MockMvcResultHandlers.print;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.status;

import java.util.Arrays;
import java.util.Date;
import java.util.List;

import org.junit.Before;
import org.junit.Test;
import org.junit.runner.RunWith;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.mockito.MockitoAnnotations;
import org.springframework.http.MediaType;
import org.springframework.test.context.ContextConfiguration;
import org.springframework.test.context.junit4.SpringJUnit4ClassRunner;
import org.springframework.test.context.web.WebAppConfiguration;
import org.springframework.test.web.servlet.MockMvc;
import org.springframework.test.web.servlet.RequestBuilder;
import org.springframework.test.web.servlet.request.MockMvcRequestBuilders;
import org.springframework.test.web.servlet.setup.MockMvcBuilders;

import kr.or.connect.guestbook.config.ApplicationConfig;
import kr.or.connect.guestbook.config.WebMvcContextConfiguration;
import kr.or.connect.guestbook.dto.Guestbook;
import kr.or.connect.guestbook.service.GuestbookService;

@RunWith(SpringJUnit4ClassRunner.class)
@WebAppConfiguration
@ContextConfiguration(classes = {WebMvcContextConfiguration.class, ApplicationConfig.class })
public class GuestbookApiControllerTest {
    @InjectMocks
    public GuestbookApiController guestbookApiController;   // 1)

    @Mock
    GuestbookService guestbookService;                      // 2)

    private MockMvc mockMvc;

    @Before
    public void createController() {                        // 3)
        MockitoAnnotations.initMocks(this);                 // 4)
        mockMvc = MockMvcBuilders.standaloneSetup(guestbookApiController).build();  // 5)
    }

    @Test
    public void getGuestbooks() throws Exception {
        Guestbook guestbook1 = new Guestbook();             // 6)
        guestbook1.setId(1L);
        guestbook1.setRegdate(new Date());
        guestbook1.setContent("hello");
        guestbook1.setName("BOB");

        List<Guestbook> list = Arrays.asList(guestbook1);
        when(guestbookService.getGuestbooks(0)).thenReturn(list); // 7)

        RequestBuilder reqBuilder = MockMvcRequestBuilders.get("/guestbooks").contentType(MediaType.APPLICATION_JSON);  // 8)
        mockMvc.perform(reqBuilder).andExpect(status().isOk()).andDo(print()); // 9)

        verify(guestbookService).getGuestbooks(0);
    }

    @Test
    public void deleteGuestbook() throws Exception {
        Long id = 1L;

        when(guestbookService.deleteGuestbook(id, "127.0.0.1")).thenReturn(1);

        RequestBuilder reqBuilder = MockMvcRequestBuilders.delete("/guestbooks/" + id).contentType(MediaType.APPLICATION_JSON); // 10)
        mockMvc.perform(reqBuilder).andExpect(status().isOk()).andDo(print()); // 11)

        verify(guestbookService).deleteGuestbook(id, "127.0.0.1");
    }
}

```

## 3. 소스 상세보기

### 1)

```java
    @InjectMocks
    public GuestbookApiController guestbookApiController;
```

- InjeckMocks 어노테이션을 붙여서 선언된 guestbookApiController는 목객체인  
  GuestbookService를 사용하게 된다.
- 스프링을 위해 주입된 객체를 사용하는 것이 아닌 Mockito 프레임워크를 위해  
  목객체가 주입되어 생성된다.

### 2)

```java
    @Mock
    GuestbookService guestbookService;
```

- @Mock어노테이션을 붙여서 선언된 guestbookService는 mockito를 위해 목객체  
  로 생성된다 **(말 그대로 가짜 객체)**

### 3)

```java
    @Before
        public void createController() {
            .......
    }
    }
```

- 테스트 메소드가 실행되기 전에 @Before어노테이션이 붙은 메소드가 실행된다.

### 4)

```java
    MockitoAnnotations.initMocks(this);
```

- 현재 객체에서 @Mock이 붙은 필드를 목객체로 초기화시킵니다.

### 5)

```java
mockMvc = MockMvcBuilders.standaloneSetup(guestbookApiController).build();
```

- MockMVC타입의 변수 mockMvc를 초기화 합니다.
- guestbookApiController를 테스트 하기 위한 MockMvc객체를 생성합니다.

### 6)

```java
        Guestbook guestbook1 = new Guestbook();
        guestbook1.setId(1L);
        guestbook1.setRegdate(new Date());
        guestbook1.setContent("hello");
        guestbook1.setName("kim");

        List<Guestbook> list = Arrays.asList(guestbook1);
```

- List<Guestbook>타입의 변수 list를 초기화하고 해당 list에  
  방명록 한 건을 저장합니다.

### 7)

```java
    when(guestbookService.getGuestbooks(0)).thenReturn(list);
    ------------------------------------------------------------------
    when( 목객체.목객체메소드호출() ).threnReturn(목객체 메소드가 리턴 할 값)
```

- guestbookService.getGuestbook(0) 이 호출되면 위에서 선언된  
  list객체가 리턴 되도록 설정합니다.

### 8)

```java
RequestBuilder reqBuilder
 = MockMvcRequestBuilders.get("/guestbooks").contentType
                                (MediaType.APPLICATION_JSON);
```

- MockMvcRequestBuilders를 이용해 MockMvc에게 호출할 URL을 생성합니다.

```java
    get(“/guestbooks”)
```

- GET 방식으로 /guestbooks 경로를 호출하라는 의미입니다.

```java
    contentType(MediaType.APPLICATION_JSON);
```

- application/json 형식으로 api를 호출합니다.
- 즉 2가지가 합치면 application/json형식으로 /guestbooks를  
  GET방식으로 호출한다는 것을 뜻합니다.
- 이러한 URL정보를 가진 reqBuilder를 생성합니다

### 9)

```java
 mockMvc.perform(reqBuilder)
```

- reqBuilder에 해당하는 URL에 대한 요청을 보냈다는 것을 의미합니다.

```java
    .andExpect(status().isOk()).andDo(print());
```

- mockMvc에 위해 URL이 실행되고 상태코드값이 200이 나와야 한다는 것을  
  의미합니다.
- andDo(print())는 처리 내용을 출력하게 됩니다.

## 4. 테스트 결과

- junit 테스트 콘솔 창

```java

MockHttpServletRequest:
      HTTP Method = GET
      Request URI = /guestbooks
       Parameters = {}
          Headers = {Content-Type=[application/json]}

Handler:
             Type = kr.or.connect.guestbook.controller.GuestbookApiController
           Method = public java.util.Map<java.lang.String, java.lang.Object> kr.or.connect.guestbook.controller.GuestbookApiController.list(int)

Async:
    Async started = false
     Async result = null

Resolved Exception:
             Type = null

ModelAndView:
        View name = null
             View = null
            Model = null

FlashMap:
       Attributes = null

MockHttpServletResponse:
           Status = 200
    Error message = null
          Headers = {Content-Type=[application/json;charset=UTF-8]}
     Content type = application/json;charset=UTF-8
             Body = {"pageStartList":[],"count":0,"list":[{"id":1,"name":"BOB","content":"hello","regdate":1655739941313}]}
    Forwarded URL = null
   Redirected URL = null
          Cookies = []
```

## 5. deleteGuestbook TEST

### 10)

```java
RequestBuilder reqBuilder = MockMvcRequestBuilders.
    delete("/guestbooks/" + id).contentType(MediaType.APPLICATION_JSON);
```

- “/guestbooks/” + id 경로를 DELETE방식으로 호출하기 위한 경로 정보를  
  가지고 있는 reqBuilder객체를 생성합니다.

### 11)

```java
mockMvc.perform(reqBuilder).andExpect(status().isOk()).andDo(print());
```

- reqBuilder에 해당하는 URL을 호출한 후, 상태 코드가 200일 경우 성공합니다.

### 12)

```java
verify(guestbookService).deleteGuestbook(id, "127.0.0.1");
```

- Web API가 동작하면서 호출되었다면 성공하게 됩니다.

<a href="https://www.boostcourse.org/web326/lecture/59389">부스트코스</a>
