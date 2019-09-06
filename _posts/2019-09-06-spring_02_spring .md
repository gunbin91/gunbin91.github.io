---
layout: post
title: "2. Spring Framework개요"
tags: [ spring ]
date: 2019-09-06
categories: [ spring ]
---

<p align="center">
    스프링 프레임워크란 무엇인가
</p><br/>

## ◆ SPRING 프레임워크
웹 어플리케이션 제작 시 <font color="orange">MVC패턴을 쉽게 구현 할 수 있게 지원</font>해 주는 툴이다.

<br/>

#### ▶ MVC프레임워크 종류
SPRING, 전자정부프레임워크, struts 등등..<br/>
( 전자정부프레임워크 : spring기반의 국내 표준으로 주로 공공기관 프로젝트에서 많이 사용된다. )

<br/>

#### ▶ Eclipse 버전업
이클립스 <font color="hotpink">EE버전으로는 스프링을 연동할 수 없다.</font> 따라서 이클립스의 버전을 업그레이드 시키거나, 새로운 이클립스 버전으로 다운받아야 한다.<br/>
공식사이트: https://projects.spring.io ( 4.3.14 GA버전 )

<br/>

- 방법1. 이클립스 버전up
: 새로운 Eclipse를 설치하지 않고 기존 사용하던 Eclipse의 버전을 업그레이드 시키는 방법이다.<br/><font color="orange">help -> Market Place -> popular -> Spring Tools (aka Spring IDE and Spring Tool Suite) 3.9.2.RELEASE</font> 다운

<br/>

- 방법2. 이클립스 spring버전 다운
: 기존 Eclipse를 사용하지 않고 Spring이 가능한 새로운 Eclipse를 다운받는다.<br/> ( 개인적으로 로딩화면이 더 이뻐서? 추천 )<br/><a href="spring.io/tools">spring.io/tools</a>접속 => 운영체제에 맞는 버전다운( STS.exe )

> help -> about eclips에서 spring이 설치되어 있는지 확인이 가능하다.

<br/>

#### ▶ SPRING프레임워크 연동
스프링 프레임워크 또한 두 가지의 방법으로 연동을 할 수 있지만, 보통은 메이븐을 이용해서 연동 하도록 한다.

<br/>

- 방법1. 빌드패스 추가 방법
: 웹 프로젝트의 경우에는 lib파일에 jar파일만 넣으면 되지만 자바 프로젝트의 경우 빌드패스로 잡아주어야 한다.<br/> <font color="orange">프로젝트 우 클릭 -> build path -> configual build path -> libaries -> add external JAR 자르 파일추가</font>

<br/>

- 방법2. 메이븐 연동 방법
: 프로젝트 우 클릭 -> configure -> convert to Maven project 
으로 메이븐 프로젝트를 만든 후 만들어진 pom.xml파일에 추가
{% highlight ruby %}
<dependencies>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>4.3.14.RELEASE</version>
    </dependency>
</dependencies>
{% endhighlight %}

<br/>

#### ▶ SPRING 특징
- 제어 반전 컨테이너 ( IOC ≒ DI )
: 스프링은 객체들을 직접 생성해서 쓰지 않고,‘IOC 컨테이너’라는 곳에 생성 할 객체들을 설정해 두고<font color="orange"> DI(Dependency Injection)의존성 주입</font>이라는 개념으로 사용한다. 때문에 제어가 반전됐다는 뜻에서 제어반전 컨테이너라고 부른다.

- 관점 지향 프로그래밍 가능 ( AOP (AspectOrientedProgramming) )
: 코드 상에서 반복적으로 작성되는 공통적인 작업들이 많기 때문에, 이를 공통의 관점이라 보고 공통 작업들을 자동적으로 호출해주는 기능이다.

- 데이터 엑세스 지원
: 스프링에서는 데이터베이스의 접근 또한 지원해준다. 데이터베이스의 객체들 역시 IOC컨테이너에 등록시켜 두고 써야 하지만, 스프링에서는 스프링에서 지원하는 객체들로 좀 더 편하게 작업을 할 수 있도록 해준다.

- 트랜잭션 관리
: 

- MVC패턴 구현 지원
: 







<br/>