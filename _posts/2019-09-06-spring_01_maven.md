---
layout: post
title: "1. Maven(메이븐)"
tags: [ spring, maven ]
date: 2019-09-06
categories: [ spring ]
---

<p align="center">
    지금까지 여러 기능들을 사용하기 위해 라이브러리를 다운받고 프로젝트에 추가하는 번거로운 작업방식을 해왔지만, 메이븐을 이를 간단한 코드작성으로 쉽게 연동해 주는 역할을 한다.
</p><br/>

## ◆ Maven (메이븐)
Java기반 프로젝트의 라이프 사이클 관리를 목적으로 하는 빌드 도구<br/>
컴파일과 빌드를 동시에 수행, 테스트를 병행하거나 서버 측 Deploy지원을 관리할 수 있는 환경을 제공

<br/>

#### ▶ 라이브러리 관리 기능 내포
개발 시 다양한 라이브러리를 필요로 하게 되는데, 메이븐 이용시 <font color="hotpink">pom.xml파일에 필요한 라이브러리만 적으면 Maven이 알아서 다운받고 설치</font>해주고 경로까지 지정해 준다.<br/>
=> 즉, 여태까지 라이브러리에 jar파일등을 추가하는 방식과 달리 메이븐을 이용하여 라이브러리를 연동하는 것

<br/>

## ▶ 설정 방법

#### 1. Maven프로젝트 생성
New->Maven Project를 통해 새로 만들거나 또는<br/><font color="orange">이미 만들어진 프로젝트를 우 클릭-> configure -> convert to Maven project</font>로 변환
<br/>
#### ※ Maven POM작성
- group id : 사용자별로 설정 ( 아무거나 )
- artifact id : 프로젝트별로 설정 ( 아무거나 통일 )

#### ※ 에러 시 대처
Maven의 설정파일은 <font color="hotpink">C:사용자/.m2</font> 디렉토리 안에 다 되어있기 때문에 
에러가 생길 경우 이 디렉토리를 지우고 다시 시도하면 된다.

<br/>

#### 2. pom.xml 라이브러리 추가
메이븐 프로젝트를 생성하거나 convert하게 되면 <font color="orange">pom.xml</font>이라는 파일이 자동 생성된다.
해당 파일에서 밑의 탭들 중에 pom.xml탭을 선택하고 라이브러리 사이트에서 배포하는 <font color="orange">메이븐 배포코드</font>를 복사해서 &lt;dependencies>태그 안에 붙여 넣어주면 된다.
<br/>

ex ) SPRING연동 예
{% highlight ruby %}
<dependencies>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>4.3.14.RELEASE</version>
    </dependency>
</dependencies>
{% endhighlight %}
&lt;/build>태그 밖으로 추가한다.

- 메이븐은 스프링뿐만 아니라 대부분의 라이브러리를 연동할 수 있으며, 대부분의 라이브러리 배포사이트에서 jar파일과 별도로 pom.xml설정코드를 같이 배포한다.
<br/><br/>
- 또한 <font color="orange">여러 개의 라이브러리를 추가할 때</font> &lt;dependencies>를 여러 개 추가하는 것이 아니라, 하나의 &lt;dependencies>태그 안에 <font color="orange">&lt;dependency>만 여러 개 추가</font>해서 여러 라이브러리를 추가한다.
<br/>

ex ) gson을 추가로 추가
{% highlight ruby %}
<dependencies>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>4.3.14.RELEASE</version>
    </dependency>
    
    <dependency>
        <groupId>com.google.code.gson</groupId>
        <artifactId>gson</artifactId>
        <version>2.8.2</version>
    </dependency>
</dependencies>
{% endhighlight %}

- 메이븐을 이용하여 라이브러리를 추가하게 되면, 빌드패스를 이용해 jar파일을 추가하는 방식과 같이 <font color="orange">자동적으로 메이븐 라이브러리에 jar파일이 추가</font> 된다 <br/>
( 단, 인터넷이 연결되어 있는 상태이어야 함! )
<br/><br/>
- oracle에서 배포하는 라이브러리는 메이븐에서의 다운로드를 막아두었기 때문에 메이븐에서 사용할 수 없고, jar파일을 다운로드하여 빌드패스로 추가할 수밖에 없다.

<br/>

#### ▶ 라이브러리 모음 사이트
개발자 편의를 위해 라이브러리를 모아둔 사이트
<a href="http://mvnrepository.com/">http://mvnrepository.com/</a><br/>
라이브러리 검색 후 해당 라이브러리 다운로드에서 
메이븐 탭을 보면 메이븐 설정파일도 있다.








<br/>