---
layout: post
title: "7. DataBase Access지원( Mybatis연동 )"
tags: [ spring, mybatis ]
date: 2019-09-17
categories: [ spring ]
---

<p align="center">
    Spring에서는 데이터베이스 접근객체 역시 IOC에 등록해 두고 사용한다.<br/> 스프링에서 지원하는 데이터베이스 접근객체와 마이바티스 연동방법에 대해 알아보자. 
</p><br/>

## ◆ 데이터 엑세스 지원 ( DB작업 지원 )
스프링에서도 데이터베이스 접근객체가 따로 있다.<br/><font color="hotpink">
    DB 작업 지원 (Connection 관리 / CRUD / transaction / DB Framework 와의 연동)</font><br/>
but 국내 표준은 마이바티스이기 때문에 <font style="text-decoration:underline hotpink;">스프링에서 지원하는 데이터베이스작업으로는 거의 하지 않는다.</font><br/>
( 스프링과 마이바티스를 연동하여 사용 )

<br/>

## ◆ Connection지원
스프링에서 자체적으로 지원하는 데이터베이스 접근 객체를 이용하여 데이터베이스 제어를 해보자.

### ▶ 메이븐 다운로드
- spring jdbc
{% highlight ruby %}
<!-- https://mvnrepository.com/artifact/org.springframework/spring-jdbc -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-jdbc</artifactId>
    <version>4.3.14.RELEASE</version>
</dependency>
{% endhighlight %}

- commons dbcp 
{% highlight ruby %}
<!-- https://mvnrepository.com/artifact/commons-dbcp/commons-dbcp -->
<dependency>
    <groupId>commons-dbcp</groupId>
    <artifactId>commons-dbcp</artifactId>
    <version>1.4</version>
</dependency>
{% endhighlight %}

- ojdbc.jar
: 빌드패스 - 익스터널 jar - ojdbc8 추가

<br/>

### ▶ IOC컨테이너 등록
- &nbsp;<font color="orange">DriverManagerDataSource</font>
: DB정보를 입력하고 등록하는 객체로 <font color="orange">Mybatis와 연동 할 때에도 필요</font>하다.
{% highlight ruby %}
<bean id="ds"
class="org.springframework.jdbc.datasource.DriverManagerDataSource">
    <property name="driverClassName">
        <value>oracle.jdbc.driver.OracleDriver</value>
    </property>
    <property name="url" value="jdbc:oracle:thin:@192.168.10.80:1521:xe" />
    <property name="username">
        <value>root</value>
    </property>
    <property name="password">
        <value>oracle</value>
    </property>
</bean>
{% endhighlight %}

- &nbsp;<font color="orange">jdbcTemplate</font>
: 생성자의 인자로 DataSource를 받아 데이터베이스의 CRUD작업을 할 수 있는 객체<br/>
기존의 jdbc에서 Connection객체와 PreparedStatements객체로 하던 작업들을 Spring에서는 해당 객체로 통합적으로 작업한다.
{% highlight ruby %}
<bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
    <property name="dataSource" ref="ds"></property>
</bean>
{% endhighlight %}

- 사용할 객체 등록
: 스프링에서는 모든 객체를 주입받는 형식으로 작업하기 때문에, Jdbc Tmplate객체를 필드로하는 클래스를 또 만들 필요가 있다.
{% highlight ruby %}
<bean id="cs" class="data.alpha.CouponService">
    <constructor-arg name="template" ref="jdbcTemplate"></constructor-arg>
</bean>
{% endhighlight %}
=> 필드로 jdbcTemplate객체를 설정해두고 쓴다.

<br/>

### ▶ 연결
{% highlight ruby %} 
ApplicationContext ctx = new ClassPathXmlApplicationContext("스프링설정파일경로");
DataSource ds = ctx.getBean(DataSource.class); // DriverManagerDataSource의 상위객체
Connection conn = ds.getConnection();
{% endhighlight %}
객체등록 후 컴파일완료가 되었다면, Connection객체가 하는 일을 jdbcTemplate가 해주기 때문에 Connection객체를 생성할 필요는 없지만 생성은 가능하다.

<br/>

## ◆ CRUD지원

### ▶ jdbcTemplate객체 사용
jdbcTemplate은 PreparedStatements객체를 사용하지 않고 해당 객체 하나로 모든 작업을 하기때문에 String형의 SQL문을 사용하여 바로바로 작업한다.

- PreparedStatement의 executeUpdate() [ C U D ]
: &nbsp;=  <font color="orange">jdbcTemplate객체.update()</font>
- PreparedStatement의 executeQuery() [ R ] 
: &nbsp;=  <font color="orange">jdbcTemplate객체.query()</font>

<br/>

### ▶ 사용 예제
{% highlight ruby %}
JdbcTemplate template;
template.update("insert into coupon values(?,?,?,?)", serial, limit, max, cnt);
{% endhighlight %}
 ? 에 넣을 데이터들을 PreparedStatements객체로 설정하는 것이 아닌
콤마(,)를 구분자로 두 번째 인자부터 차레 대로 데이터들을 넣어주는 형태가 된다.

> jdbcTemplate객체는 <font color="orange">spring에서 자동적으로 open()이나, close()등의 작업</font>을 해주기 때문에 수동으로 작업할 필요가 없다. 단 마이바티스에서도 Template객체가 있기 때문에 크게 사용하지 않는 추세이다.

<br/>

## ◆ 스프링의 마이바티스 연동
실질적으로 데이터베이스작업은 JdbcTemplate객체가 아닌 마이바티스로 연동하여
하는 작업을 주로 하게 된다.

### ▶ 메이븐 라이브러리 다운
- MyBatis
{% highlight ruby %}
<!-- https://mvnrepository.com/artifact/org.mybatis/mybatis -->
<dependency>
    <groupId>org.mybatis</groupId>
    <artifactId>mybatis</artifactId>
    <version>3.4.5</version>
</dependency>
{% endhighlight %}

- MyBatis Spring
{% highlight ruby %}
<!-- https://mvnrepository.com/artifact/org.mybatis/mybatis-spring -->
<dependency>
    <groupId>org.mybatis</groupId>
    <artifactId>mybatis-spring</artifactId>
    <version>1.3.1</version>
</dependency>
{% endhighlight %}

<br/>

### ▶ IOC컨테이너 객체등록
- DriverManagerDataSource
: DriverManagerDataSource는 마이바티스에서도 필요하다.
{% highlight ruby %}
<bean id="ds"
class="org.springframework.jdbc.datasource.DriverManagerDataSource">
    <property name="driverClassName" value="oracle.jdbc.driver.OracleDriver" />
    <property name="url" value="jdbc:oracle:thin:@192.168.10.80:1521:xe" />
    <property name="username" value="root" />
    <property name="password" value="oracle" />
</bean>
{% endhighlight %}

<br/>

- &nbsp;<font color="orange">SqlSessionFactoryBean</font>
: SqlSessionFactory는 인터페이스이기 때문에 SqlSessionFactoryBuild를 이용하여 객체를 생성해야 하므로 한번에 등록이 어렵다.<br/>
때문에 스프링에서는 <font color="orange">등록용 객체인 SqlSessionFactoryBean객체를 등록하여 SqlSessionFactory객체로 캐스팅하여 사용</font>한다.

{% highlight ruby %}
<bean id="factory" class="org.mybatis.spring.SqlSessionFactoryBean">
    <property name="dataSource" ref="ds"></property>
    <property name="mapperLocations">
        <list>
            <value>classpath:mappers/place-mapper.xml</value>
        </list>
    </property>
</bean>
{% endhighlight %}
- dataSource필드에 DriverManagerDataSource객체값을 넘겨준다.
- mapperLocations필드에 Sql Mapper작업 xml파일의 경로를 list로 넘겨준다.

> 스프링에서 <font color="hotpink">xml파일의 경로를 찾을 때는 classpath:로 시작해야 인식</font>할 수 있으며, 절대경로로 인식하기 때문에 /로  시작할 필요는 없다.<br/>
단, WebContent아래의 경로들은 src와 인식을 다르게 하기 때문에 xml파일을 찾을 때 classpath:로 시작할 필요는 없다.

<br/>

## ◆ SqlSessionTemplate
SqlSessionFactory를 직접 뽑아서 쓰게 되면, 다시 SqlSession객체를 뽑아내야 하고 해당 객체로 close()등의 작업들도 직접 해야한다.<br/>

하지만 <font color="orange">SqlSessionTemplate객체를 사용하게 되면 자동으로 openSession(), close()등의 작업을 처리</font> 해주기 때문에 이러한 부분들을 신경 쓸 필요가 없어진다.<br/>
( 실질적으로도 보통 이 객체를 이용해 데이터베이스작업을 하게 된다. )

<br/>

### ▶ 객체등록
SqlSessionTemplate객체는 생성자의 인자로 SqlSessonFactory를 받기 때문에 등록해 둔 SqlSessionFactoryBean객체를 넘겨준다.
{% highlight ruby %}
<bean id="sqlTemplate" class="org.mybatis.spring.SqlSessionTemplate">
    <constructor-arg name="sqlSessionFactory">
        <ref bean="factory" />
    </constructor-arg>
</bean>
{% endhighlight %}
해당 SqlSessionTemplate객체로 기존 SqlSession객체로 하던 작업을 할 수 있다.

- <a href="/jsp/2019/09/03/jsp_17_mybatis1.html" style="text-decoration:none;">Mybatis사용법</a>



<br/>