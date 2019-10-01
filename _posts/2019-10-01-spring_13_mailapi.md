---
layout: post
title: "13. JAVA Mail API"
tags: [ spring, mailAPI, spring메일 보내는법 ]
date: 2019-10-01
categories: [ spring ]
---

<p align="center">
    타 SMTP서버를 이용하여 메일을 보내는 방법에 대해 알아보자.
</p><br/>


## ◆ Java Mail API
스프링에서 제공되는 것이 아닌 자바에서 제공되는 Mail API를 이용하여 e메일을 보내는 것이 가능하다.<br/>단, <font color="hotpink">메일을 보내기 위해서는 SMTP라는 메일 서버가 필요</font>한데, 구글에서 이를 제공해 주고 있기 때문에 <font color="hotpink">자체SMTP서버가 없을 시 구글계정을 사용</font>할 수 있다.

<br/>

### ▶ 메이븐 연동
#### 1. javax.mail
{% highlight ruby %}
<!-- https://mvnrepository.com/artifact/javax.mail/mail -->
<dependency>
    <groupId>javax.mail</groupId>
    <artifactId>mail</artifactId>
    <version>1.4.7</version>
</dependency>
{% endhighlight %}

#### 2. Spring Context Support
{% highlight ruby %}
<!--
 https://mvnrepository.com/artifact/org.springframework/spring-context-support -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context-support</artifactId>
    <version>4.3.14.RELEASE</version>
</dependency>
{% endhighlight %}

> 메일을 외부로 전송하기 위해선 SMTP서버가 필요하다. 단 자체 SMTP서버를 구축하지 못하는 상황에서는 네이버SMTP 또는 구글SMTP서버등을 이용해서 작업할 수 있다.

<br/>

### ▶ 구글 SMTP사용법

<br/>

#### 1. 구글 계정 로그인
구글의 SMTP를 사용하기 위해 로그인 과정이 필요하기 때문에 구글의 계정정보를 입력해야 하는데, 타 앱프로그램에서 로그인하는 것이 기본적으로 막혀있기 때문에 <font color="orange">계정의 보안수준을 낮추는 작업이 필요</font>하다.
- 보안수준 변경: <a href="https://myaccount.google.com/lesssecureapps?utm_source=google-account&utm_medium=web">https://myaccount.google.com/lesssecureapps?utm_source=google-account&utm_medium=web</a>

<br/>

#### 2. 스프링 설정파일(IOC)에 MailSender객체 등록
{% highlight ruby %}
<!-- 메일 센더 -->
<bean class="org.springframework.mail.javamail.JavaMailSenderImpl">
	<!-- ip대신 -->
	<property name="host" value="smtp.gmail.com"></property>
	<!-- 구글계정 -->
	<property name="username" value="구글계정아이디"></property>
	<!-- 구글계정 비밀번호 -->
	<property name="password" value="구글계정비밀번호"></property>
	<property name="port" value="587"></property>
	<property name="javaMailProperties">
		<props>
            <prop key="mail.smtp.starttls.enable">true</prop>
		</props>
	</property>
</bean>
{% endhighlight %}
※ property로 설정 할 수 있는 것들은 더 있지만 디폴트 설정이 있기 때문에 위에 정보만 필수적으로 입력해 두면 된다.

<br/>

### 3. 객체 사용
아래 코드를 서비스객체등을 통해 적절히 사용하면 된다.
{% highlight ruby %}
@Autowired
JavaMailSender mailSender;

public boolean sendWelcomMail(String target) {
	MimeMessage message = mailSender.createMimeMessage();
	try {
		// 받는사람
		message.setRecipient(RecipientType.TO, new InternetAddress(target));
		// 보내는 사람 - google서버같은경우는 이 설정을 무시함
		message.setFrom(new InternetAddress("administrator@spring.io"));
		// 메일제목
		message.setSubject("[SpringIO] 가입을 축하드립니다.");
		// 메일내용
		String content = "가입을 축하드립니다.\n밤바바밤밤";
		message.setContent(content, "text/plain;charset=utf-8");
		// content설정을 text/html로 하게되면 HTML로 전송할 수도 있다.
		// 보내기
		mailSender.send(message);
		return true;
	} catch (AddressException e) {
		e.printStackTrace();
		return false;
	} catch (MessagingException e) {
		e.printStackTrace();
		return false;
	}
}
{% endhighlight %}




<br/>