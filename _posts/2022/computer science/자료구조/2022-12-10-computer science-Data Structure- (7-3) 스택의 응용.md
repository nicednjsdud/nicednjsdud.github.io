---
title: (자료구조) 7-3 스택의 응용
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 스택의 응용
tag: Internet
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,자료구조
last_modified_at: "2022-12-10 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 자료 구조 - 스택의 응용

## 1. 시스템 스택

### 1) 프로그램에서의 호출과 복귀에 따른 수행 순서

1. 가장 나중에 호출된 함수가 가장 먼저 실행을 완료하고 복귀하는 **후입선출** 구조이므로, 함수의 호출과  
   복귀 순서는 스택의 **LIFO 구조**를 응용하여 관리

2. 함수 호출이 발생하면 호출된 함수 수행에 필요한 **지역변수, 매개 변수 및 수행 후 복귀할 주소** 등의  
   정보를 스택 프레임(stack frame)에 저장하여 시스템 스택에 삽입

3. 시스템 스택의 **top은 현재 실행중인 함수가 호출되었을 때 이에 대한 전환 정보가 들어있는 스택 프레임이 됨**

4. 함수의 실행이 끝나면 시스템 스택의 top 원소(스택 프레임)를 삭제(pop)하면서 스택 프레임이  
   저장되어 있던 복귀 주소를 확인하고 복귀

5. 함수 호출과 복귀에 따라 이 과정을 반복하여 전체 프로그램 수행이 종료되면 시스템 스택 은 공백 스택이 됨

![alt](/assets/images/post/ComputerStudy/392.png)

## 2. 수식의 괄호 검사

- 수식에 포함되어 있는 괄호는 가장 마지막에 열림 괄호를 가장 먼저 닫아 주어야 하는 후입 선출  
  구조로 구성되어 있으므로 후입선출 구조의 스택을 이용하여 괄호를 검사함
- 수식을 왼쪽에서 오른쪽으로 하나씩 읽으면서 괄호 검사
  - 왼쪽 괄호를 만나면 스택에 push
  - 오른쪽 괄호를 만나면 스택을 pop하여 마지막에 저장한 괄호와 같은 종류인지를 확인
- 같은 종류의 괄호가 아닌 경우 괄호의 짝이 잘못 사용된 수식임
- 수식에 대한 검사가 모두 끝났을때 스택은 공백 스택이됨
- 수식이 끝났어도 스택이 공백이 되지 않으면 괄호의 개수가 틀린 수식임

## 3. 수식의 후위표기와 계산

### 1) 수식을 표현하는 방법

- 전위 표기법 : 연산자를 피연산자 앞에 표기하는 방법 **예) +AB**
- 중위 표기법 : 연산자를 피연산자의 가운데에 표기하는 방법 **예) A+B**
- 후위 표기법 : 연산자를 피연산자의 뒤에 표기하는 방법 **예) AB+**

### 2) 중위 표기식을 전위 표기식으로 변환 방법

1. 수식의 각 연산자에 대해서 우선순위에 따라 괄호를 사용하여 다시 표현함
2. 각 연산자를 그에 대응하는 왼쪽 괄호의 앞으로 이동시킴
3. 괄호를 제거함

![alt](/assets/images/post/ComputerStudy/402.png)

### 3) 중위 표기식을 후위 표기식으로 변환 방법

1. 수식의 각 연산자에 대해서 우선순위에 따라 괄호를 사용하여 다시 표현함
2. 각 연산자를 그에 대응하는 오른쪽 괄호의 앞으로 이동시킴
3. 괄호를 제거함

![alt](/assets/images/post/ComputerStudy/403.png)

### 4) 스택을 사용하여 중위 표기식을 후위 표기식으로 변환

1. 왼쪽 괄호를 만나면 무시하고 다음 문자를 읽음
2. 피연산자를 만나면 출력함
3. 연산자를 만나면 스택에 push함
4. 오른쪽 괄호를 만나면 스택을 pop하여 출력함
5. 수식이 끝나면 스택이 공백이 될 때까지 pop하여 출력함

### 5) 후위 표기법 변환 알고리즘

```c
  infix_to_postfix(exp)
    while(true) do{
        sysbol <- getSysbol(exp);
        case {
          symbol = operand :        // 피연산자 처리
                print(symbol)
          symbol = operator :       // 연산자 처리
                push(stack, symbol);
          symbol = ")" :            // 오른쪽 괄호 처리
                print(pop(stack));
          symbol = null :           // 수식의 끝 처리
                while(top > -1) do
                      print(pop(stack));
          else :
        }
    }
end infix_to_postfix()
```

### 6) 스택을 사용하여 후위 표기식을 연산

1. 피연산자를 만나면 스택에 push 함
2. 연산자를 만나면 필요한 만큼의 피연산자를 스택에서 pop하여 연산하고, 연산결과를 다시 스택에 push함
3. 수식이 끝나면, 마지막으로 스택을 pop하여 출력함

- 수식이 끝나고 스택에 마지막으로 남아있는 원소는 전체 수식의 연산 결과 값이 됨

```c
  evalPostfix(exp)
    while(true) do{
        sysbol <- getSysbol(exp);
        case {
          symbol = operand :        // 피연산자 처리
                push(Stack, symbol);

          symbol = operator :       // 연산자 처리
                opr2 <- pop(Stack);
                opr1 <- pop(Stack);
                result <- opr1 op(symbol) opr2;
                // 스택에서 꺼낸 피연산자들을 연산자로 연산
                push(Stack,result);

          symbol = null :           // 수식의 끝
                print(pop(stack));
          else :
        }
    }
end infix_to_postfix()
```
