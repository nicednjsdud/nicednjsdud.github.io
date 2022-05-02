---
title: Java 17. Collection FrameWork
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Java
description: What is collection framework?
tag : java language
article_tag1: java
article_section: java
meta_keywords: java,java language, collection framework
last_modified_at: '2022-04-02 12:00:00 +0800'
toc: true
toc_sticky: true
toc_label: 목차
---

Collection Framework
======================

## 1.컬렉션 프레임워크

* 프로그램 구현에 필요한 자료구조와 알고리즘 구현해 놓은 라이브러리
* java.util 패키지에 구현되어 있음.
* 개발에 소요되는 시간을 절약하고 최적화된 라이브러리를 사용할 수 있음.
* Collection 인터페이스와 Map 인터페이스로 구성됨.

## 2.Collection Interface

* 하나의 객체의 관리를 위해 선언된 인터페이스
* 필요한 기본 메서드가 선언되어 있음    
* 컬렉션 하위에 List, Set 인터페이스가 있음.

### List 인터페이스

* 순서가 있는 자료 관리, 중복 허용

```
    - 객체를 순서에 따라 저장하고 관리하는데 필요한 메서드가 선언된 인터페이스. 
```

- 구현한 클래스

```
    - ArrayList, Vector, LinkedList, Stack, Queue 등이 있음.
```

```java
import java.util.LinkedList;

public class LinkedListTest {

	public static void main(String[] args) {
		
		LinkedList<String> myList = new LinkedList<>();
		myList.add("A");
		myList.add("B");
		myList.add("C");
		System.out.println(myList.toString()); // [A,B,C]
		
		myList.add(1, "D");
		System.out.println(myList); // [A,D,B,C]
		
		myList.removeLast();
		System.out.println(myList); // [A,D,B]
		
		for(int i=0;i<myList.size();i++) {
			String s = myList.get(i);
			System.out.print(s+" ");		// A,D,B
		}
		
	}

}   
```  

```java
import java.util.ArrayList;

class MyStack{
	//ArrayList로 Stack구현
	private ArrayList<String> arrayStack = new ArrayList<>();	
	
	public void push(String data) {
		arrayStack.add(data);
	}
	// 후입선출
	public String pop() {
		int len = arrayStack.size();
		if(len == 0) {
			System.out.println("스택이 비었습니다.");
			return null;
		}
		return arrayStack.remove(len-1);		// 0부터 시작하니 -1해줌
	}
}
public class StackTest {

	public static void main(String[] args) {
		MyStack stack = new MyStack();
		stack.push("A");
		stack.push("B");
		stack.push("C");
		String remove=stack.pop();
		System.out.println(remove);     // C
	}
}
```

## Set 인터페이스

- 순서가 정해져 있지 않음, 중복을 허용하지 않음.
- 맴버의 중복 여부를 체크하기 위해 인스턴스의 동일성을 확인해야 함.
- 동일성 구현(논리적인 동등)을 위해 필요에 따라 equals()와 hashCode() 메서드를 재정의함.
- 유일한 값을 관리하는데 필요한 메서드 선언됨.

```
    - 아이디, 주민번호, 사번 등을 관리하는데 유용
```

### 구현한 클래스
* HashSet, TreeSet 등이 있음.

### TreeSet 클래스

- 객채의 정렬에 사용되는 클래스
- 중복을 허용하지 않으면서 오름차순이나 내린차순으로 객체를 정렬함.
- 내부적으로 이진 검색 트리(binary search tree)로 구현되어 있음
- 이진 검색 트리에 자료가 저장될 때 비교하여 저장될 위치를 정함.
- 객체 비교를 위해 comparable이나 comparator 인터페이스를 구현해야함.
- 비교 대상이 되는 객체에 comparable이나 comparator 인터페이스를 구현해야 TreeSet에  
  추가 될수 있음.

- String, Integer 등 JDK의 많은 클래스들이 이미 Comparable를 구현했음. 


## HashSet

```java
import java.util.HashSet;

public class HashSetTest {
	public static void main(String[] args) {
		HashSet<String> set = new HashSet<>();
		set.add("이순신");
		set.add("하륜");
		set.add("이방원");
		set.add("이순신");		// 중복 x 체크
		System.out.println(set); // [이순신, 하륜, 이방원]		
	}
}   
```  
## TreeSet
```java
import java.util.TreeSet;

public class TreeSetTest {

	public static void main(String[] args) {
		TreeSet<String> treeSet = new TreeSet<>();
		treeSet.add("정도전");
		treeSet.add("최영");
		treeSet.add("이순신");
		
		for(String s : treeSet) {			// 오름차순
			System.out.println(s);			// 이순신, 정도전, 최영
		}
	}

}
```
## 3.Map Interface

* 쌍으로 이루어진 객체를 관리하는데 필요한 여러 메서드가 선언되어 있음.

* Map을 사용하는 객체는 key-value 쌍으로 되어 있고 key는 중복x

### 검색을 위한 자료구조

- key를 이용하여 값을 저장하거나 검색, 삭제할 때 사용하면 편리함.
- 내부적으로 hash 방식으로 구현 됨.

* key가 되는 객체는 객체의 (논리적)유일성함의 여부를 알기 위해  
       equals()와 hashCode() 메서드를 재정의 함.

## 구현한 클래스

- Hashtable, HashMap, TreeMap

- HashMap 클래스

```
    - Map 인터페이스를 구현한 클래스 중 가장 일반적으로 사용하는 클래스
    - pair 자료를 쉽고 빠르게 관리할 수 있음.
```

- Properties


* TreeSet logic

```java
import java.util.HashMap;
import java.util.Iterator;

public class MemberHashMap {
	
	private HashMap<Integer, Member> hashMap;
	public MemberHashMap() {
		hashMap =new HashMap<>();
	}
	
	public void addMember(Member member) {
		hashMap.put(member.getMemberId(), member);	// 추가
	}
	
	public boolean removeMember(int memberId) {		// 제거
		if(hashMap.containsKey(memberId)) {
			hashMap.remove(memberId);
			return true;
		}
		System.out.println("회원번호가 없습니다.");
		return false;
	}
	public void showAllMember() {
		Iterator<Integer> ir = hashMap.keySet().iterator();// key값만 set방식으로 리턴
		while(ir.hasNext()) {
			int key = ir.next();
			Member member = hashMap.get(key);
			System.out.println(member);
		}
		System.out.println();
		
	}
}        
```

## 4.Iterator (Collection 요소를 순회) 

* 컬레션 프레임워크에 저장된 요소를 하나씩 차례대로 참조하는 것.
* 순서가 있는 list 인터페이스의 경우는 Iterator를 사용하지 x  

```
       get() 메서드를 활용할 수 있음.
```

* Set 인터페이스의 경우 get() 메서드가 제공되지 않으므로 Iterator를 활용하여 객체를 순회함

### Iterator 사용하기
* boolean hasNext() 

```
    - 이후에 요소가 더 있는지를 체크하는 메서드.
    - 요소가 있다면 true를 반환
```

* E next()

```
    - 다음에 있는 요소를 반환.
```

```java
import java.util.HashSet;

public class HashSetTest {
	public static void main(String[] args) {
		HashSet<String> set = new HashSet<>();
		set.add("이순신");
		set.add("하륜");
		set.add("이방원");
		set.add("이순신");		// 중복 x 체크
		System.out.println(set); // [이순신, 하륜, 이방원]		
	
Iterator<String> ir = set.iterator();
		
		while(ir.hasNext()) {
			String str =ir.next();
			System.out.print(str+" "); // 이순신 하륜 이방원
		}
    }    
```  

* Member 셋팅

```java
public class Member {
	
	private int memberId;
	private String memberName;
	
	public Member() {};
	public Member(int memberId,String memberName) {
		this.memberId=memberId;
		this.memberName=memberName;
	}
	public int getMemberId() {
		return memberId;
	}
	public void setMemberId(int memberId) {
		this.memberId = memberId;
	}
	public String getMemberName() {
		return memberName;
	}
	public void setMemberName(String memberName) {
		this.memberName = memberName;
	}
	@Override
	public String toString() {
		return memberName +"회원님의 아이디는"+memberId+"입니다.";
	}
	@Override
	public int hashCode() {
		System.out.println("hashCode() 호출");
		return memberId;
	}
	@Override
	public boolean equals(Object obj) {
		if(obj instanceof Member) {
			Member member = (Member)obj;
			return this.memberId==member.memberId;
		}
		return false;
	}
}
```

* HashSet logic

```java
import java.util.HashSet;
import java.util.Iterator;

public class MemberHashSet {
	
	private HashSet<Member> hashSet;
	
	public MemberHashSet() {
		hashSet=new HashSet<Member>();	// 기본생성자에서 초기화
	}
	public void addMember(Member member){				//추가
		hashSet.add(member);
	}
	
	public boolean removeMember(int memberId) {			// 삭제
		Iterator<Member> ir = hashSet.iterator();
		while(ir.hasNext()) {
			Member member=ir.next();
			if(member.getMemberId()==memberId) {
				hashSet.remove(member);
				return true;
			}
		}
		System.out.println(memberId+" 번호가 존재하지 않습니다.");
		return false;
	}
	public void showAllMember() {				// 전체보기
		for(Member member: hashSet) {
			System.out.print(member+" ");
		}
		System.out.println();
	}
}
```

* Member 셋팅

```java
public class Member implements Comparator<Member> {
    ...
    ...

    /*
	 *  id로 정렬함 
	 *  양수면 오름차순 *(-1) 곱해주면 내림차순 정렬
     *  implements Comparator<Member>
	 */
	@Override
	public int compare(Member member1, Member member2) {
		return (member1.memberId- member2.memberId);
	}
}
``` 

* TreeSet logic

```java
import java.util.Iterator;
import java.util.TreeSet;

import kr.co.ezenac.treeset2.Member;

public class MemberTreeSet {
	
	private TreeSet<Member> treeset;
	public MemberTreeSet() {
		treeset = new TreeSet<>(new Member());			// 기본생성자에서 초기화
	}
	public void addMember(Member member) {		// 추가
		treeset.add(member);
	}
	public boolean removeMember(int memberId) {		// 삭제
		Iterator<Member> ir = treeset.iterator();
		while(ir.hasNext()) {
			Member member = ir.next();
			if(member.getMemberId()==memberId) {
				treeset.remove(member);
				return true;
			}
		}
		System.out.println(memberId +"번호가 존재하지 않습니다.");
		return false;
	}
	public void showAllMember() {				// 전체보기
		for(Member member: treeset) {
			System.out.println(member);
		}
		System.out.println();
	}
}
```

