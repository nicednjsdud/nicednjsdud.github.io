---
title: Java 16. Collection FrameWork
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- java
description: What is collection framework?
tag : java language
article_tag1: java
article_section: java
meta_keywords: java,java language, collection framework
last_modified_at: '2022-04-01 12:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

Collection Framwork
====================

## 1.자료구조

* 대량의 데이터를 효율적으로 관리하는 메커니즘.
* 우편번호, 학교에서 학생들을 관리하는 경우.

```
    - 무작위 명단 => 특정 학생을 찾는 것은 비효율적
    - 학년, 반, 출석번호를 사용한 체계적인 관리를 통해 특정 학생을 찾는 경우 효율적임.
```

### 배열 
* 배열은 크기가 고정되어 있어 데이터를 추가하거나 삭제는 불가.

```
    - 새로 배열을 만들고 옮겨야 함.
```

### 리스트 
- 원소가 원소를 가리켜서 관리하는 자료구조.
- 데이터가 추가, 삭제될 때 연결하는 정보만 바꾸면 쉽게 처리됨.

### 스택 
- 선형구조(LIFO, Last In First Out)

### 큐 (파이프에 물나가는 구조)
- 선형구조(FIFO, First In First Out)      

### 트리
- 부모 노드와 자식 노드간의 연결로 이루어진 자료 구조
- 부모 노드 밑에 여러 자식 노드가 연결되고, 자식 노드 각각에 다시 자식 노드가 연결되는 형태의 자료구조.
- 이진 검색 트리(binary search tree)

```
         - 부모노드에 자식노드가 두개 이하인 트리  
```

## 2.컬렉션 프레임워크

```
    Iterable<E> <- Collection<E> <- List<E>,Set<E>,Queue<E>,Map<K,V> 
```

### List<E>

* 순서가 있는 데이터 집합.
* 추가된 데이터의 순서도 유지되며, 데이터 중복도 허용됨.
* 구현 클래스 

```
    - ArrayList
    - LinkedList
    - Vector
    - Stack
```

### List<E> 인터페이스를 구현하는 컬렉션 클래스들 
- ArrayList<E> : 배열기반 자료구조. 배열을 이용하여 객체를 저장함.
    
```    
    - 데이터가 여러 개 쭉 있는 것을 표현한 것임.
    - 예) 데이터 목록(List) 좀 뽑아주세요 ~
```

- 데이터의 저장 순서가 유지됨.
- 동일 데이터의 중복 저장 허용됨.

## 3.객체 배열을 구현한 클래스 ArrayList

### 기존 배열
- 선언과 사용 방식은 배열의 길이를 정하고 요소의 개수가 배열의 길이보다  
  커지면 배열을 재할당하고 복사해야 했음.
- 배열의 요소를 추가하거나 삭제하면 다른 요소들의 이동에 대한 구현해야 함.

### ArrayList
- 객체 배열을 좀더 효율적으로 관리하기 위해 자바에서 제공해 주는 클래스
- 최적의 알고리즘으로 구현되어 있어 사용 방법만 익히면 유용하게 사용가능 하다.

### 주요 메서드 

- boolean add(E e)

```
    - 요소 하나를 배열에 추가함.
```        

- int size()

```
    - 배열에 추가된 요소 전체 개수를 반환함.
```

- E get(int index)

```
    - 배열의 index 위치에 있는 요소 값을 반환함.
```

- E remove(int index)

```
    - 배열의 index 위치에 있는 요소 값을 제거하고 그 값을 반홤함.
```

- boolean isEmpty()

```
    - 배열이 비어 있는지 확인함.
``` 

* Student

```java
import java.util.ArrayList;

public class Student {
	
	int StudnetID;
	String studentName;
	ArrayList<Subject> subjectList;
	
	public Student(int studnetID, String studentName) {
		
		StudnetID = studnetID;
		this.studentName = studentName;
		subjectList = new ArrayList<>();
	}
	
	public void addSubject(String name,int scorePoint) {
		Subject subject =new Subject();
		subject.setName(name);
		subject.setScorePoint(scorePoint);
		subjectList.add(subject);
	}
	
	public void showInfo() {
		int total =0;
		for(Subject s: subjectList) {
			total += s.getScorePoint();
			System.out.println("학생 " +studentName+"의 " + s.getName() +"과목 성적은"
					+s.getScorePoint()+"입니다.");
			
		}
		System.out.println("학생 "+studentName+ " 의 총점은 "+total+"이다.");
	}
	
	
}
```

* subject

```java
public class Subject {
	
	private String name;
	private int scorePoint;
	
	

	
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public int getScorePoint() {
		return scorePoint;
	}
	public void setScorePoint(int scorePoint) {
		this.scorePoint = scorePoint;
	}
	
	
}
```

* Test

```java
public class StudentTest {

	public static void main(String[] args) {
		
		Student studentLee = new Student(2022, "이순신");
		studentLee.addSubject("국어",100);
		studentLee.addSubject("수학", 90);
		
		Student studentShin = new Student(2020,"신사임당");
		studentShin.addSubject("국어", 90);
		studentShin.addSubject("수학", 99);
		studentShin.addSubject("영어", 91);
		
		studentLee.showInfo();
		System.out.println();
		studentShin.showInfo();
	}

}
```
