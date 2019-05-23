---
layout: post
title: "7. 내장객체와 리스너"
tags: [ jsp, session, application, listener ]
date: 2019-05-22
categories: [ jsp ]
---

<p align="center">
    JSP에서는 기본적으로 내장되어 있는 객체가 있고, 많이 사용하는 객체들이다. 자세하게 알아보자.
</p><br/>

# ◆ 내장객체 ( Implicit Object ) 
서블릿으로 처리할 때 요청 처리 중에 사용할 수 있는 객체가 매개변수로 설정된 ServletRequest, ServletResponse 객체 두개가 있는데, JSP는 스크립트릿( <% %> )에서 사용할 수 있는 객체가 8개 +@(exception)가 있다.

## 1. page ( final java.lang.Object page = this; )
jsp에서 this를 사용하게 되면 해당 객체를 의미한다. ( 거의 사용 안함 )

<br/>

## 2. config ( final javax.servlet.ServletConfig config;  - config )
config에는 Servlet 작성 시 init에서 사용했던 config객체 값이 담겨져 있다. 하지만 이것도
활용빈도가 없다. 왜냐하면, ServletConfig는 init-param을 확보하는데 사용되는데, JSP로
요청 처리 할 때는 init-param을 설정할 타이밍이 없음.

<br/>

## 3. out ( javax.servlet.jsp.JspWriter out = null;  - out )
out객체는 응답을 전송할 때 사용되는 출력 객체이다. <br/>
서블릿에서 뽑아서 사용하던 PrintWriter의 역할과 같은 역할이지만, JSP에서 out객체는 JspWrite객체이다. 마찬가지로 <font color="orange">out.println()</font>메서드를 이용하여 출력한다.

<br/>

## 4. request ( HttpServletRequest request )
서블릿에서 사용되던 ServletRequest을 확장시킨 객체.<br/>
핵심 용도는 사용자의 요청 정보에 대한 접근 시 사용됨 ( ServletRequest 보다 기능이 많다. )<br/>
=> 서블릿에서 사용하고 싶을 경우 (HttpServletRequest)로 캐스팅해서 사용할 수 있다.<br/>
ex) (HttpServletRequest)request

<br/>

#### ▶ HttpServletRequest의 주요 메서드들
- String addr = request.getRemoteAddr();
: 요청클라이언트의 ip주소 반환
- StringBuffer sb = request.getRequestURL();
: 주소창에 입력한 url 전체를 반환 ( 풀경로 )
- String protocol = request.getProtocol();
: http: 또는 https 인지 확인
- String ctxPath = <font color="orange">request.getContextPath();</font>
: 프로젝트명 반환( 경로설정 시 많이 사용된다. )
- String uri = request.getRequestURI();
: ip를 제외한 경로 반환
- String query = request.getQueryString();
: 주소창에서 보내는 '?' 뒤에 부분을 전부다 뽑아내는 메서드
- String method = <font color="orange">request.getMethod();</font>
: 요청 메서드 반환 ( GET, POST ) -  일반적으로 GET을 많이 쓴다. 
- String mode = <font color="orange">request.getParameter("");</font>
: 특정이름의 값들을 뽑아내는 메서드
- String[] num = <font color="orange">request.getParameterValues("");</font>
: 특정이름의 값들을 배열로 뽑아내는 메서드( 값이 여러개일 때 사용 )
- HttpSession s = request.getSession();
: jsp가 아닌곳에서 세션객체를 뽑아내는 메서드<br/>
( 서블릿에는 세션객체가 기본적으로 내장되어있지 않기 때문에 
(HttpServletRequest)request.getSession()을 이용하여 세션을 뽑아내 사용할 수 있다. )
> getReuqestURL,URI 는 경로만 반환하고, ? 뒤에 파라미터들을 반환하지 않는다.

<br/>

## 5. response ( HttpServletResponse )
서블릿에서 사용되던 ServletResponse을 확장시킨 객체 JSP에서 쓰는 response객체의 메서드가 서블릿에서는 안 보일 수도 있음. 핵심 용도는 사용자의 응답 정보에 대한 접근 설정 시 사용됨

<br/>

#### ▶ HttpServletResponse 메서드
- response.<font color="orange">sendRedirect("페이지");</font>
: 페이지이동 메서드이다.
<br/>=> out.clear() 가 자동적으로 되기 때문에 현재 페이지에서 설정한 내용은 볼 수 없고 바로 설정한 페이지로 넘어간다. ( 서블릿 객체인 ServletResponse는 해당 메서드를 사용 할 수 없다. )<br/>
> sendRedirect를 하게 되면 밑에 코드 또한 모두 실행되고 진행된다. 따라서 밑에 코드를 실행하지 않으려면 return; 이 필요하다.

- Response.addCookie(Cookie c) 
: 쿠키등록
- getCharacterEncoding() 
: 응답 문자 인코딩 형태를 반환

<br/>

## 6. session ( javax.servlet.http.HttpSession session = null; )
session객체는 <font color="orange">서버가 클라이언트별로 생성 시켜 저장하는 데이터 저장용 객체</font>이다. <br/><font color="hotpink">형태는 Map<String,Object></font>를 사용한다.<br/>
( 쿠키와 달리 서버에 저장되며, 저장 용량의 제한이 없다. )<br/>

#### ▶ session 특징
- 웹 프로그램을 사용하는 클라이언트들은 무조건 하나의 세션을 부여 받게 됨.(프로젝트 당 하나)<br/>
한번 생성된 세션은 일정시간동안 재접속(아무런 작업을)을 안하게 되면, 해제가 된다. 그 전까지는 계속 유지

- 어느 페이지를 접속하던 간에 하나만 생성됨으로 같은 서버 다른 페이지 접속 시에도 세션은 새로 생성되지 않음

- 브라우저가 다르면 다른 클라이언트로 인식, 브라우저를 끄는 순간에도 세션이 해제된다. 단, 같은 브라우저가 여러 개 켜져 있을 시 다 끄지 않는 이상 세션은 유지된다. 

#### ▶ session 객체 주요 메서드
- session.isNew() 
: 세션이 새로 생성되었는지 확인<br/> 
( 각각의 클라이언트가 최초 접근 시에만 생성됨으로 isNew는 최초 접근시에만 true )
- session.getId() 
: 세션 아이디값 String반환
- session.<font color="orange">setAttribute("변수",Object);</font>
: 세션의 변수 값을 하나 지정
- session.<font color="orange">getAttribute("변수");</font>
: 세션에 지정해 둔 변수값을 반환<br/>
=> Object형으로 저장되기 때문에 캐스팅해서 사용한다. 없으면 null 반환<br/> 
( 없으면 null이 저장되고 컴파일 오류는 아니지만 if문 등에서 비교 시 null이면 에러 )
- session.getAttributeNames();
: 세션에 저장된 name을 Enumeration객체로 반환 아래와 같이 사용할 수 있다
{% highlight ruby %}
Enumeration e = session.getAttributeNames();
while(e.hasMoreElements()){
String name = e.nextElement().toString();
	String value = session.getAttribute(name).toString();
	out.println(name + " // " + value + "<br/>");
}
{% endhighlight %}
- session.<font color="orange">removeAttribute("변수);</font>
: 세션 객체에 지정해 둔 객체를 제거
- session.getMaxInactiveInterval();
: 세션의 유지시간 (초단위) int형 반환
- session.<font color="orange">setMaxInactiveInterval(int sec);</font>
: 세션의 유지시간(초단위)를 일시적으로 변경<br/>
=> 영구적으로 변경하기 위해서는 서버디렉터리/conf/web.xml에서 설정
{% highlight ruby %}
<session-config>
<session-timeout>5</session-timeout> <!-- 분단위  -->
</session-config>
{% endhighlight %}
- session.getCreationTime();
: 세션이 생성된 시간을 ms단위로 반환
- session.invalidate();
: 세션을 완전히 해제시킴 <br/>
=> invalidate() 밑에 코드에서 session객체는 해제되었기 때문에 사용할 수 없고, 페이지 이동시에는 다시 새로운 세션이 생성된다.

<br/>

## 7. application ( final javax.servlet.ServletContext application; )
ServletContext객체는 WAS가 프로그램에 부여하는 단 하나의 유일 객체. 따라서 <font color="orange">모든 클라이언트가 공유할 수 있는 객체</font>이다.<br/>
웹 프로그램에 필요한 설정이나 웹 프로그램 상태 확인 등을 할 수 있다.<br/>

#### ▶ application 특징
- 내장객체로 잡혀 있지만 request.getServletContext()메서드를 통하여 뽑아낼 수 있으며,
 이렇게 뽑아낸 객체는 application과 같은 객체이다.
- application.getInitParameter(“title”)은 서블릿의 init메서드에서 사용하던 config.getInitParam()과 비슷한 메서드이다. web.xml 에서 아래 형식으로 등록하게 되면 param-name이라는 이름으로 value값을 뽑아낼 수 있다.
{% highlight ruby %}
<context-param>
<param-name>title</param-name>
<param-value>어플리케이션</param-value>
</context-param>
{% endhighlight %}

- 보통 프로그램 전반에서 사용하게 될 값들을 저장시켜 놓는 용도로 쓰임.

- application.getMajorVersion(); application.getMinorVersion(); 서블릿 버전을 알 수 있다.
(메이저).(마이너) 버전 
- application도 session객체와 같이 <font color="orange">set/get/remove Attribute</font> 메서드가 있다.
차이점은 applicaton객체의 Attribute는 모든 클라이언트가 공유된다.

#### ▶ application 메서드
- application.getRealPath("파일명");  
: 해당 파일의 실제 경로를 반환 
- application.getResourceAsStream("파일명") 
: 해당 파일을 Stream 객체로 반환하여 in/out 을 바로 할 수 있게 해주는 메서드
- applicaton.log("메시지");
: 이클립스에서 돌리는 테스트가상서버에서는 동작하지 않고, war파일로 export 시켜서 가동시켜야 작동된다. log파일 확인 및 기록
<br/>
( ex ) D:\17_10_Web_Jogunbin2\workspace\.metadata\.plugins\org.eclipse.wst.server.core\tmp0\logs)

<br/>
 
## 8. pageContext (final javax.servlet.jsp.PageContext pageContext )
PageContext라는 객체는 직접 제어 할 상황 상황은 많지 않음.<br/>
JSP에서 Servlet으로 변환 시에, 내장 객체들을 쉽게 확보할 수 있게 설계해 둔 객체이다. Servlet에서는 존재하지 않는 JSP파일에서만 사용가능한 객체.<br/>
{% highlight ruby %}
<%=pageContext.getOut() == out%>
<%=pageContext.getSession() == session%>
=> pageContext.include("~~.jsp");
{% endhighlight %}
pageContext에서도 include가 가능하지만, 해당 파일의 출력만 담당하기 때문에 include지시어와 달리 해당 파일에 있었던 변수 등을 쓸 수 없다.

## @. Throwable exception
해당페이지가 에러 페이지일 때만 생성되는 객체로, 에러에 대한 메시지를 확인할 수 있다.

<br/>

# ◆ 웹페이지 리스너 등록
리스너는 페이지내에서 구현하기 어려운 타이밍에 대한 문제를 해결하기 위해 사용한다. 리스너는java Resources -> src 에 생성한다.<br/>

## ▶ 리스너 작성법
#### 1. 리스너를 구현하는 클래스 작성 
#### 2. web.xml에 리스너 등록 :
{% highlight ruby %}
<listener>
    <listener-class>리스너 클래스</listener-class>
</listener>
{% endhighlight %}

<br/>

## ▶ Reqeust리스너
페이지 요청 시작과 페이지 구축이 완료될 때 호출되는 메서드를 작성할 수 있다.<br/>
즉 각각 페이지 접근 시 마다 호출되는 메서드<br/>
1. <font color="hotpink">implements ServletRequestListener</font>을 구현하는 클래스를 생성
2. public void requestInitialized(ServletRequestEvent e) 
3. public void requestDestroyed(ServletRequestEvent e) 

<br/>

## ▶ session 리스너
세션 리스너는 <font color="hotpink">implements HttpSessionListener</font>을 구현하는 클래스를 생성하면 된다.<br/>
( <font color="orange">세션의 생성과 해제 타이밍에 호출</font>되기 때문에 접속 중인 클라이언트수를 구하는 등에 많이 사용 )<br/>

- 오버라이드 메서드에 매개인자로 있는 <font color="orange">Evenet객체를 이용하여 getSession 하면 해당 클라이언트의 세션을 얻어 올 수 있다.</font>
- 세션은 브라우저를 끄면 소멸되지 않고, 세션 안에 담겨져 있던 정보가 날아가기만 하기 때문에 브라우저를 껐다 키면 새로운 세션이 생성된다. ( 즉, 소멸은 되지 않고 생성만 됨 )
-> 소멸은 invalidate() 메서드를 쓰거나, 세션 유효시간 초과 시에만 소멸된다.

<br/>

## ▶ session 의 get,set Attribute 리스너
<font color="hotpink">implemnets HttpSessionAttributeListener</font> 을 구현하는 클래스는
세션의 set/get Attribute 할 때 작동하는 메서드를 만들 수 있다.<br/>

- attributeRepleaced메서드는 set된 데이터를 또 set (교체) 할  때 호출된다.
- 이벤트객체.getName
: 하게되면 set될 때 키로 설정한 값을 반환 하게 된다.
- 이벤트객체.getValue 
: setAttribute할때의 벨류값

> implements HttpSessionBindingListener 도 같은역할.. 
( session.put 을 해야 작동( session.setAttribute 의 예전메서드 ) 
=> session.getAttribute로 뽑아낼 순 있다. )

<br/>
## ▶ application 리스너
&nbsp;<font color="orange">서버가 켜지고 꺼질 때 작동</font>되는 메서드 <font color="hotpink">implements ServletContextListener</font> 구현 클래스
- 공유데이터를 저장하거나, 불러올 때 유용

- ServletContextAttributeListener 
: session과 마찬가지로 Attribute 리스너가 있다.

> 리스너는 implements로 구현하기 때문에 동시에 여러개 처리 또한 가능하다.









<br/>