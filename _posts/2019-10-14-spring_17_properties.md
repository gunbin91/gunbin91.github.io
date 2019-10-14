---
layout: post
title: "17. Properties 설정"
tags: [ spring, properties ]
date: 2019-10-14
categories: [ spring ]
---

<p align="center">
    
</p><br/>

## ◆ Properties
Properties는 DB설정과 같은 <font color="hotpink">설정 정보들을 소스코드와 분리해서 설계하기 위해</font> 사용한다.

<br/>

### ▶ Properties작성법
Properties파일은 일반 File로 만들어서 ~.properties로 작성한다.
<br/>ex) jdbc.properties<br/>
아래와 같이 각 정보의 구분자를 개행으로 하여 간단하게 작성한다.
{% highlight ruby %}
jdbc.driver=core.log.jdbc.driver.OracleDriver
jdbc.url=jdbc:oracle:thin:@localhost:1521:xe
jdbc.username=system
jdbc.password=oracle
{% endhighlight %}

<br/>

### ▶ Properties객체를 사용하여 설정값 불러오기
소스코드에서 Properties파일의 설정정보를 불러올 수 있도록 자바에서는 Properties객체를 지원한다.

{% highlight ruby %}
import java.util.Properties;
...

public static void main(String[] args) {
    String resource = "config/jdbc.properties"; // Properties파일의 경로
    Properties properties = new Properties();
    
    try {
        Reader reader = Resources.getResourceAsReader(resource);
        properties.load(reader);

        System.out.println(properties.getProperty("jdbc.driver"));
        System.out.println(properties.getProperty("jdbc.username"));
        System.out.println(properties.getProperty("jdbc.password"));
        System.out.println(properties.getProperty("jdbc.url"));
    } catch (IOException e) {
        e.printStackTrace();
    }
}
{% endhighlight %}

<br/>

## ◆ Spring에서 Properties사용하기
Spring에서는 Properties값들을 좀 더 쉽게 불러올 수 있도록 지원한다.

### ▶ @Value 어노테이션을 이용하여 Properties불러오기
- 시스템정보
: 시스템 정보는 별도의 Properties파일 등록 없이도 아래와 같이 불러올 수 있다.
{% highlight ruby %}
@Value("#{systemProperties['os.name']}") private String name;
// => Window10
{% endhighlight %}

<br/>

- Properties파일 정보
: Properties파일의 정보를 불러오기 위해서 Spring설정 파일에서 아래와 같이 
&lt;context:property-placeholder>태그를 통하여 Properties파일 경로를 잡아야한다.<br/>
Spring설정 파일에 Properties파일 경로를 잡아준 후에 아래와 같이 Properties의 속성값을 사용할 수 있다.
{% highlight ruby %}
// spring bean
<context:property-placeholder location="/WEB-INF/db.properties" />
// controller
@Value("${jdbc.username}") private String username;
{% endhighlight %}

<br/>

### ▶ Spring설정 파일에서 사용
- &lt;<font color="orange">context:property-placeholder</font> location="db.properties" />
: <context:property-placeholder>태그로 등록한 값들은 불러올 때 값이 치환되어 들어가기 때문에 Properties파일에 해당 값이 없더라도 예외가 발생하지 않고 입력한 그대로를 치환해준다.(단점)
<br/>불러올 때는 <font color="orange">${속성명}</font>를 이용하여 불러온다.
{% highlight ruby %}
<bean id="dataSource" class="org.apache.tomcat.jdbc.pool.DataSource">
    <property name="driverClass" value="${jdbc.driverclass}"/>
    ...
</bean>
{% endhighlight %}

<br/>

- &lt;<font color="orange">util:properties</font> id="pro" location="db.properties"/>
: <util:properties>태그를 이용하여 Properties를 사용하게 될 경우 단순히 값을 치환하여 가져오는 것이 아니라, 해당 Properties를 bean으로 등록하기 때문에 예외를 발생시켜 줄 수 있다.
<br/>불러올 때는 <font color="orange">#{id['속성명']}</font>으로 불러온다.
{% highlight ruby %}
<bean id="dataSource" class="org.apache.tomcat.jdbc.pool.DataSource">
    <property name="driverClass" value="#{pro['db.driverclass']}"/>
    ...
</bean>
{% endhighlight %}





<br/>