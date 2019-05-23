---
layout: post
title: "8. 액션태그와 자바빈"
tags: [ jsp, action tag, javabean ]
date: 2019-05-22
categories: [ jsp ]
---

<p align="center">
    jsp에서만 사용하는 액션태그와 자바빈에대해 알아보자.
</p><br/>

# ◆ 액션태그
jsp페이지 내에서 어떤 동작을 하도록 지시하는 태그

#### ▶ forward
URL을 유지시킨 채 <font color="orange">현재 페이지를 다른 페이지로 전환(포워딩)</font>시킬 때 사용되는 액션 태그<br/>
URL은 접근한 페이지 그대로 유지되지만, 실제로 보여지는 페이지는 포워드로 설정한 페이지이다.
{% highlight ruby %}
<jsp:forward page=”sub.jsp”/>  // sub.jsp페이지로 이동
{% endhighlight %}

> 주의) 태그를 꼭 닫아주거나, 태그 끝에 /로 열고 닫음을 동시처리 해야한다.

<br/>

#### ▶ param
forward액션태그를 사용할 때 같이 사용되는 태그로 <font color="orange">포워드될 페이지로 파라미터를 보내는 액션태그</font>이다.<br/>
파라미터는 request.getParameter(“name”)으로 반환할 수 있다. 
{% highlight ruby %}
<jsp:forward page="sub.jsp">
	<jsp:param value="cho" name="id"/>
	<jsp:param value="1234" name="pass"/>
</jsp:forward>
{% endhighlight %}

<br/>

#### ▶ include
현재 페이지 내에 해당 코드가 삽입 된 부분에 해당 페이지를 삽입하는 액션태그이다.<br/>
=> include지시어와 같은 기능이다.
{% highlight ruby %}
<jsp:include page=”sub.jsp”/>
{% endhighlight %}

<br/>

# ◆ 자바빈
<br/>

#### ▶ 빈(bean)
자바 언어의 데이터(속성)과 기능(메서드)로 이루어진 클래스이다.

<br/>

#### ▶ 빈 만들기
 Java Resources->src에 자바클래스로 객체를 만든다. 데이터(속성)을 만든 후 속성에 해당하는 getter, setter을 모두 만들어준다.

#### ▶ 빈 관련 액션태그
- useBean
: 빈 객체를 사용하겠다는 태그로 New를 통한 생성이 필요 없이 선언하는 용도.<br/>
id : 해당 객체를 제어할 수 있는 고유 값, 변수정도로 생각하면 된다.<br/>
class : 빈 객체의 경로를 적어준다. 경로는 .으로 구분<br/>
Scope: 객체를 사용할 범위를 지정하는 속성으로 4가지의 값이 있다.<br/>
(page-생성된 페이지 내에서만, request-요청된 페이지 내에서만, session-웹 브라우저의 생명 주기와 동일하게, application-웹 어플리케이션 생명 주기와 동일하게)
{% highlight ruby %}
<jsp:useBean id="student" class="com.java.Student" scope="page"/>
{% endhighlight %}
<br/>

- setProperty
: 데이터 값을 설정할 때 사용<br/>
name : useBean에 설정한 id를 적어주어 설정할 빈객체 선택<br/>
property : 해당 빈 객체의 속성명 <br/>
value: 해당 속성에 적용할 값<br/>
{% highlight ruby %}
<jsp:setProperty name="student" property="name" value="홍길동"/>
{% endhighlight %}
<br/>

> setproperty의 경우 넘어오는 파라미터의name과 property의 이름이 일치 할 경우 value가 자동 세팅 되며 property를 *로 하는 경우 모든 일치하는 속성값을 세팅해준다.

<br/>

- getProperty
: 데이터 값을 불러올 때 사용, 바로 출력되는 형식이다.
{% highlight ruby %}
<jsp:getProperty name="student" property="name"/>
{% endhighlight %}










<br/>