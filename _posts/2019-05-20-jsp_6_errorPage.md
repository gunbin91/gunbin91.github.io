---
layout: post
title: "6. 예외페이지"
tags: [ jsp, errorPage ]
date: 2019-05-20
categories: [ jsp ]
---

<p align="center">
    페이지 에러 발생 시 사용자 측 입장을 고려해 조금 더 그럴듯한 페이지가 될 수 있도록 에러페이지를 꾸밀 수 있는 방법에 대해 알아보자.
</p><br/>

# ◆ 예외페이지
페이지 작업 중 코드의 문제가 있어 에러페이지를 발생시키는 경우가 있다. 기본적으로 설정되어 있는 에러페이지의 경우 사용자로부터 불쾌감이 들기 때문에 해당 에러페이지를 예외페이지를 만들어 처리할 수 있다.

<br/>

## ▶ 예외 페이지 설정법
<br/>

#### 1. 예외페이지 설정
에러가 발생할 가능성이 있는 페이지에 <font color="orange">페이지 지시어의 errorPage속성을 이용하여 에러 발생 시 연결될 에러페이지를 설정</font>해준다.<br/>
<b>ex ) <%@ page errorPage="연결할 에러페이지 경로"%></b>

{% highlight ruby %}
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8" errorPage="errhome.jsp"%>
<%-- 에러발생 -->
<% int a = 40/0; %> 
{% endhighlight %}

<br/>

#### 2. 예외페이지 제작
위 errorPage속성으로 들어올 수 있는 페이지는 <font color="orange">페이지 지시어의 속성 isErrorPage가 true</font>인 페이지만 가능하다. 또한 이 속성이 <font color="ornage">true일 경우에만 exception객체를 사용</font>할 수 있게 된다.<br/>
<b>ex) <%@ page isErrorPage="true"%></b>

{% highlight ruby %}
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8" isErrorPage="true"%>

<h1> 해당 페이지는 에러페이지 입니다.</h1>
<% response.setStatus(200); %>
<%= exception.getMessage() %>
{% endhighlight %}


> 주의) 에러 페이지에서는 response.setStatus(200);을 설정해 두는 것이 좋다. 이는 해당 페이지가 정상페이지라는 것을 의미하는데, 간혹 에러페이지의 status가500으로 인식되는 경우 에러가 난 페이지로 간주되기 때문이다.

<br/>

## ▶ web.xml을 이용한 status별 예외 페이지 설정법
Web.xml에 status별 예외페이지를 등록하여 작성할 수도 있다.<br/>
이때 페이지지시어의 errorPage, isErrorPage 등은 사용하지 않는다.

{% highlight ruby %}
<error-page>
  	<error-code>404</error-code>
  	<location>/err404.jsp</location>
  </error-page>
  
  <error-page>
  	<error-code>500</error-code>
  	<location>/err500.jsp</location>
</error-page>
{% endhighlight %}
위와 같이 등록하게 되면 해당 에러코드 발생 시 지정한 에러페이지로 이동하게 된다.








<br/>