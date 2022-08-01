---
title: (Spring) 7. MyBatis XML 연동
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Spring
description: MyBatis XML 연동
tag: MyBatis
article_tag1: Spring Web
article_section: Spring Web
meta_keywords: Spring, backend ,framework
last_modified_at: "2022-07-08 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# Spring-Mybatis (XML 연동)

## 1. 스프링 - 마이바티스 연동 XML 파일 설정

### 1) 프로퍼티(Property) 파일을 이용한 설정 방법

#### 1-1 환경에 따라 자주 변경되는 내용의 분리

- DB 연결정보는 애플리케이션이 동작하는 환경에 따라 자주 바뀔수 있음
  - 환경 : 개발, 테스트, 스테이징, 운영
- 자주 변경되는 값들은 Properties 파일로 분리
  - 키와 값이 쌍(key=value)으로 구성하면 됨.
- 프로퍼티 파일로 분리한 정보는 `${} (프로퍼티 치환자)`을 이용하여 설정함.

## 2. 연동방법

### 1) action-mybatis.xml 생성

- WEB-INF/config/action-mybatis.xml 생성

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns:context="http://www.springframework.org/schema/context"
	xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
		http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-3.1.xsd">

	<!-- PropertyPlaceholderConfigurer 클래스 이용해 db 설정 관련 정보를 jdbc.properties 파일에서 읽어 들임 -->
	<bean id="propertyPlaceholderConfigurer"
					class="org.springframework.beans.factory.config.PropertyPlaceholderConfigurer">
		<property name="locations">
			<value>/WEB-INF/config/jdbc.properties</value>
		</property>
	</bean>

	<!-- PooledDataSource 이용해서 dataSource 빈 생성 -->
	<bean id="dataSource" class="org.apache.ibatis.datasource.pooled.PooledDataSource">
		<property name="driver" value="${jdbc.driverClassName}" />
		<property name="url" value="${jdbc.url}"/>
		<property name="username" value="${jdbc.username}"/>
		<property name="password" value="${jdbc.password}"/>
	</bean>

	<!-- SqlSessionFactoryBean 클래스 이용해  dataSource 속성에 dataSource 빈을 설정-->
	<!-- configLocation 속성에 modelConfig.xml을 설정 -->
	<!-- mapperLocations 속성에 mybatis/mappers 패키지의 모든 매퍼 파일들을 읽어 들여와 설정 -->
	<bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
		<property name="dataSource" ref="dataSource" />
		<property name="configLocation" value="classpath:mybatis/model/modelConfig.xml" />
		<property name="mapperLocations" value="classpath:mybatis/mappers/*.xml" />
	</bean>

	<!-- SqlSessionTemplate 클래스를 이용해 sqlSession 빈을 생성  -->
	<bean id="sqlSession" class="org.mybatis.spring.SqlSessionTemplate">
		<constructor-arg index="0" ref="sqlSessionFactory"></constructor-arg>
	</bean>

	<!-- sqlSession 빈을 memberDAO빈 속성에 주입함 -->
	<bean id="memberDAO" class="kr.co.springmybatis.dao.MemberDAOImpl">
		<property name="sqlSession" ref="sqlSession" ></property>
	</bean>
</beans>

```

### 2) jdbc.properties 생성

- action-mybatis.xml 와 같은 위치

```
jdbc.driverClassName=oracle.jdbc.driver.OracleDriver
jdbc.url= [db url]
jdbc.username= [db username]
jdbc.password= [db password]
```

### 3) mapper 생성

- ex) member.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper
  PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
  "http://mybatis.org/dtd/mybatis-3-mapper.dtd">

<mapper namespace="mapper.member">						<!-- member.xml의 네임스페이스 지정 -->

	<resultMap type="memberDTO" id="memResult">	<!-- SQL문 실행한 후 반환되는 레코드들을 typeAlias에서 지정한 memberDTO 빈에 저장 -->
		<result property="id" column="id" />	<!-- 레코드의 컬럼 이름에 대해 memberDTO의 같은 속성에 값을 설정 -->
		<result property="pwd" column="pwd" />
		<result property="name" column="name" />
		<result property="email" column="email" />
		<result property="joinDate" column="joinDate" />
	</resultMap>

	<!--select-->											<!-- resultMap: 반환되는 레코드를 memResult에 저장함 -->
	<select id="selectAllMemberList" resultMap="memResult"> <!-- id: dao에서 id를 이용해 해당 SQL 호출 -->
		<![CDATA[
			SELECT * FROM T_MEMBER ORDER BY JOINDATE DESC
		 ]]>
	</select>

	<!-- id : MemberDAO에서 접근시 사용할 id -->
	<!-- resultType : sql문 조회 결과 이름을 호출한 메서드로 반환함 -->
	<select id="selectName" resultType="String" >
		<![CDATA[
			SELECT NAME FROM T_MEMBER WHERE ID = 'lee'
		]]>
	</select>

	<select id="selectPwd" resultType="String" >
		<![CDATA[
			SELECT PWD FROM T_MEMBER WHERE ID = 'lee'
		]]>
	</select>

	<!-- id: MemberDAO에서 호출하는 id를 지정함 -->
	<!-- resultType : 조회되는 한개의 레코드를 memberDTO에 저장함 -->
	<!-- parameterType : MemberDAO에서 SQL문 호출 시 전달되는 매개변수의 데이터 타입 지정-->
	<!-- #{id} : MemberDAO에서 메서드 호출하면서 parameterType으로 전달된 매개변수 이름을 select문의 id의 조건값으로 사용함 -->
	<select id="selectMemberById" resultType="memberDTO" parameterType="String">
		<![CDATA[
			SELECT * FROM T_MEMBER WHERE ID = #{id}
		]]>
	</select>

	<select id="selectMemberByPwd" resultMap="memResult" parameterType="int">
		<![CDATA[
			SELECT * FROM T_MEMBER WHERE pwd = #{pwd}
		]]>
	</select>

<!-- 	<select id = "searchMember" parameterType="memberDTO" resultMap="memResult">
		공통 SQL문
		<![CDATA[
			SELECT * from T_MEMBER
		]]>
		<where>
			<if test="name !='' and name !=null">
				name = #{name}
			</if>
			<if test="email !='' and email !=null">
				and email = #{email}
			</if>
		</where>
			order by joinDate desc

	</select> -->
		<select id = "searchMember2" parameterType="memberDTO" resultMap="memResult">
		<!-- 공통 SQL문  -->
		<![CDATA[
			SELECT * from T_MEMBER
		]]>
		<where>	<!-- where 태그 이용해 sql문 where절 구성함 -->
			<choose>
			<!-- name과 email 속성 값이 모두 있는 경우 name 속성 값	and email 속성 값이 있는 조건식을 where절에 추 -->
				<when test=" name !='' and name !=null and email !='' and email !=null">
					name = #{name} and email = #{email}
				</when>
				<when test=" name !='' and name !=null">
					name = #{name}
				</when>
				<when test=" email !='' and email !=null">
					email = #{email}
				</when>
			</choose>
		</where>
			order by joinDate desc

	</select>

	<!-- insert -->
	<!-- parameterType: MemberDAO에서 회원 정보를  memberDTO의 속성에 저장해서 넘김-->
	<insert id="insertMember" parameterType="memberDTO">
		<![CDATA[
			INSERT INTO T_MEMBER (id, PWD, NAME, EMAIL)
			VALUES (#{id}, #{pwd}, #{name}, #{email} )
		]]>
	</insert>

	<!-- parameterType : MemberDAO에서 회원정보를 HashMap에 담아서 전달함 -->
	<insert id="insertMember2"  parameterType="java.util.HashMap">
		<![CDATA[
			INSERT INTO T_MEMBER (id, PWD, NAME, EMAIL)
			VALUES (#{id}, #{pwd}, #{name}, #{email} )
		]]>
	</insert>

	<!-- Update -->
	<!-- parameterType :SQL문에 사용될 데이터를 memberDTO에 담아서 전달함 -->
	<update id="updateMember" parameterType="memberDTO">
		<![CDATA[
			UPDATE T_MEMBER SET PWD = #{pwd}, NAME= #{name}, EMAIL = #{email} WHERE ID = #{id}
		]]>
	</update>

	<!-- Delete -->
	<delete id="deleteMember" parameterType="memberDTO">
		<![CDATA[
			DELETE t_member WHERE id = #{id}
		]]>
	</delete>
</mapper>
















```

### 4) sqlMapConfig 생성

- sqlMapConfig.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE configuration
  PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
  "http://mybatis.org/dtd/mybatis-3-config.dtd">

<configuration>
	<!-- 마이바티스에서 데이터 전달에 사용될 memberDTO 빈을 설정 -->
	<typeAliases>
		<typeAlias type="kr.co.springmybatis.dto.MemberDTO" alias="memberDTO"/>
	</typeAliases>
</configuration>
```
