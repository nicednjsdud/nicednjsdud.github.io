---
published: true
title: "BackJoon 잃어버린 괄호 1541 (Java)"
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Algorithm
description: "백준 1541번 잃어버린 괄호 문제(Java) 풀이"
tag: "BackJoon"
article_tag1: "Algorithm"
article_section: "Algorithm"
meta_keywords: "BackJoon,Algorithm,Java"
last_modified_at: "2025-02-21 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: "목차"
---

# **📌 백준 1541번 - 잃어버린 괄호 (Java)**

![백준 로고](https://d2gd6pc034wcta.cloudfront.net/images/logo@2x.png)

---

## **💡 문제 설명**

주어진 수식을 계산할 때 **괄호를 적절히 사용하여 최소값을 만드는 문제**입니다.

![alt](/assets/images/post/Algorithm/1541.png)

### **🔸 입력 예시**

```
55-50+40
```

### **🔹 출력 예시**

```
-35
```

### **📝 문제 풀이 핵심**

1. `-`를 기준으로 식을 나누면 **최소값을 만들기 쉬움**.
2. `-`로 나눠진 그룹 중 첫 번째 그룹은 그대로 더하고, **이후 그룹들은 전부 빼기**.
3. `+` 연산자는 괄호 안에서 먼저 계산됨.

---

## **📌 문제 해결 방법**

1. `-` 연산자를 기준으로 **배열로 분리**합니다.
2. 첫 번째 그룹은 그대로 더합니다.
3. 이후 그룹들은 모두 합한 후 **한 번에 빼줍니다**.

---

## **💻 Java 코드**

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Back_1541 {
    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String str = br.readLine();

        String[] splitByMinus = str.split("-");   // '-' 기준으로 나누기
        int result = sumNumbers(splitByMinus[0]);       // 첫 번째 그룹은 더하기

        for (int i = 1; i < splitByMinus.length; i++) {
            result -= sumNumbers(splitByMinus[i]);      // 이후 그룹은 모두 빼기
        }
        br.close();
        System.out.println(result);
    }

    private static int sumNumbers(String numbers) {
        String[] splitByPlus = numbers.split("\\+");  // '+' 기준으로 나누기
        int sum = 0;
        for (String num : splitByPlus) {
            sum += Integer.parseInt(num);
        }
        return sum;
    }
}
```

---

## **📌 코드 설명**

### **🔹 1) 입력 처리**

```java
BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
String str = br.readLine();
```

- `BufferedReader`를 사용하여 입력을 빠르게 처리합니다.

---

### **🔸 2) '-' 연산자를 기준으로 나누기**

```java
String[] splitByMinus = str.split("-");
```

- `-` 연산자를 기준으로 문자열을 분리합니다.
- 예를 들어 `"55-50+40"` → `["55", "50+40"]`로 나눠집니다.

---

### **🔹 3) 첫 번째 그룹은 그냥 더하기**

```java
int result = sumNumbers(splitByMinus[0]);
```

- 첫 번째 그룹은 **괄호 없이 덧셈만 수행**합니다.

---

### **🔸 4) 이후 그룹들은 모두 빼기**

```java
for (int i = 1; i < splitByMinus.length; i++) {
    result -= sumNumbers(splitByMinus[i]);
}
```

- `-` 이후의 그룹들은 모두 덧셈을 수행한 후 **한 번에 빼줍니다**.
- 이렇게 하면 **최소값을 만들 수 있음**.

---

### **🔹 5) sumNumbers() 함수 (숫자 더하기)**

```java
private static int sumNumbers(String numbers) {
    String[] splitByPlus = numbers.split("\\+");  // '+' 기준으로 나누기
    int sum = 0;
    for (String num : splitByPlus) {
        sum += Integer.parseInt(num);
    }
    return sum;
}
```

- `+` 연산자는 그대로 더하면 되므로 따로 처리.
- `split("\\+")`을 사용해 `+`를 기준으로 나누고, 각각 더함.

---

## **🚀 실행 예시**

### **✔ 입력**

```
55-50+40
```

### **✔ 과정**

1. `splitByMinus` → `["55", "50+40"]`
2. `sumNumbers("55")` → `55`
3. `sumNumbers("50+40")` → `90`
4. `result = 55 - 90 = -35`

### **✔ 출력**

```
-35
```

---

## **📌 시간 복잡도 분석**

- **문자열 분할(split)** → O(N)
- **숫자 변환 및 연산** → O(N)
- **최종 시간 복잡도**: **O(N)** (매우 빠름)

---

## **🔹 정리**

✔ **핵심 아이디어**: `-` 이후 그룹은 괄호로 묶어 최대한 크게 만든 후 빼기  
✔ **시간 복잡도**: **O(N)**으로 매우 효율적  
✔ **자주 실수하는 부분**:

- `split("\\+")`처럼 정규 표현식에서 `+`는 이스케이프(`\\+`) 필요
- `-` 연산자가 없을 때도 고려해야 함 (`splitByMinus.length == 1` 경우)

---

## **✅ 추가로 알면 좋은 개념**

### **1️⃣ `split()`을 사용할 때 `+` 연산자의 특수성**

- `split("+")` 하면 오류 발생!
- `+`는 정규 표현식에서 **특수 문자**이므로 반드시 `split("\\+")` 사용.

### **2️⃣ `BufferedReader`를 사용할 수도 있음**

```java
BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
String expression = br.readLine();
br.close();
```

- `Scanner`보다 `BufferedReader`가 **입력 속도가 빠름**.

---

## **📢 결론**

🔹 `-` 연산자를 기준으로 나누고, **첫 번째 숫자 그룹은 더하고 이후 그룹들은 빼는 방식**으로 해결!  
🔹 **O(N)의 시간 복잡도로 매우 효율적**  
🔹 **BFS 같은 탐색이 필요 없는 단순 문자열 처리 문제**  
🔹 **자주 실수하는 부분**: `split("\\+")`와 `-`가 없는 경우 예외 처리

---

**🖋️ 더 좋은 풀이 방법이 있다면 댓글로 알려주세요! 😊**
