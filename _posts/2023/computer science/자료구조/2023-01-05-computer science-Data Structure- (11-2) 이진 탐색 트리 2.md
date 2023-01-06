---
title: (자료구조) 11-2 이진 탐색 트리 2
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 이진 탐색 트리 2
tag: Internet
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,자료구조
last_modified_at: "2023-01-05 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 자료 구조 - 이진 탐색 트리 2

## 1. 연결 자료구조를 이용한 이진 탐색 프로그램 작성 (삽입)

- 연결 자료구조를 이용한 이진 탐색의 C프로그램

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct treeNode {
      char key;                     // 데이터 필드
      struct treeNode *left;        // 왼쪽 서브 트리 링크 필드
      struct treeNode *right;       // 오른쪽 서브 트리 링크 필드
}treeNode;

typedef char element;   // char을 이진 탐색 트리 element의 자료형으로 정의

treeNode* insertNode(treeNode *p, char x)
{     // 포인터 p가 가리키는 노드와 비교화여 노드 x을 삽이하는 연산
      treeNode *newNode;
      if(p == null){
            newNode = (treeNode*)malloc(sizeof(treeNode));
            newNode -> key = x;
            newNode -> left = NULL;
            newNode -> right = NULL;
            return newNode;
      }
      else if(x < p-> key) p -> left = insetNode(p->left,x);
      else if(x > p-> key) p -> right = insertNode(p->right,x);
      else print("\n 이미 같은 키가 있습니다! \n");

      return p;
}

```

### (1) 4 ~ 8 행

- 트리노드 구조체 선언

### (2) 12 ~ 27 행

- 포인터 노드와 비교하여 단말 노드 x를 삽입하는 연산 수행

#### (2-1) else if(x < p-> key) p -> left = insetNode(p->left,x);

- 22행 : 삽입할 데이터 x가 포인터 p가 가리키는 현재 노드의 킷 값보다 작은 경우
- 포인터 p가 가르키는 현재 노드의 왼쪽 서브 트리에 대해서 삽입할 자리를 찾기 위해 insertNode() 연산을  
  재귀호출로 반복함
- 재귀호출을 수행하여 반환된 삽입 노드의 주소를 현재 노드의 왼쪽 서브트리, 즉 왼쪽 자식 노드로 설정함.

#### (2-2) else if(x > p-> key) p -> right = insertNode(p->right,x);

- 23행 : 삽입할 데이터 x가 포인터 p가 가리키는 현재 노드의 킷값보다 큰 경우
- 포인터 p가 가리키는 현재 노드의 오른쪽 서브 트리에 대해서 삽입할 자리를 찾기 위해 insertNode() 연산을  
  재귀호출로 반복함
- 재귀호출을 수행하여 반환된 삽입 노드의 주소를 현재 노드의 오른쪽 서브트리, 즉 오른쪽 자식 노드로 설정함

## 2. 연결 자료구조를 이용한 이진 탐색 프로그램 작성 (삭제)

```c
void deleteNode(treeNode *root, element key)
{     // root 노드부터 탐색하여 key 값과 같은 노드를 찾아 삭제하는 연산
      treeNode *parent, *p, *succ, *succ_parent;
      treeNode *child;

      parent = NULL:
      p = root;
      while((p != null) && (p-> key != key)){  // 삭제할 노드의 위치 탐색
            parent = p;
            if(key < p->key) p = p-> left;
            else p = p-> right;
      }
      if(p == NULL){    // 삭제할 노드가 없는 경우
            printf("\n 찾는 키가 이진 트리에 없습니다.");
            return;
      }

      // 삭제할 노드가 단말 노드인 경우
      if((p->left == NULL) && (p->right == NULL)){
            if(parent != NULL){
                  if(parent->left == p) parent->left = NULL;
                  else parent-> right = NULL;
            }
            else root = NULL;
      }

      // 삭제할 노드가 한개의 자식 노드를 가진 경우
      else if((p->left == NULL) || (p->right == NULL)){
            if(p->left != NULL) child = p->left;
            else child = p->right;

            if(parent != NULL){
                  if(parent->left == p) parent ->left = child;
                  else parent->right = child;
            }
            else root = child;
      }

      // 삭제할 노드가 두개의 자식을 가진 경우
      else{
            succ_parent = p;
            succ = p->left;
            while(succ->right != NULL){
                  succ_parent = succ;
                  succ = succ->right;
            }
            if(succ_parent->left == succ) succ_parent->left = succ->left;
            else succ_parent->right = succ->left;
            p->key = succ->key;
            p = succ;
      }
      free(p);
}
```

## 3. 연결 자료구조를 이용한 이진 탐색 프로그램 작성 (탐색)

```c
      treeNode* searchBST(treeNode* root, char x)
      {     // 이진 탐색 트리에서 키값이 x인 노드의 위치를 탐색하는 연산
            treeNode* p;
            p = root;
            while(p != null){
                  if(x < p->key) p = p->left;
                  else if (x == p->key) return p;
                  else p = p->right;
            }
            printf("\n 찾는 키가 없습니다.");
            return p;
      }
      void displayInorder(treeNode* root)
      {     // 이진 탐색 트리에서 중위 순회 화면서 출력하는 연산
            if(root){
                  displayInorder(root -> left);
                  displayInorder(root -> right);
            }
      }
```
