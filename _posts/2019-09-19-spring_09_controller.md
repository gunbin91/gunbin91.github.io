---
layout: post
title: "9. MVC패턴 구현 지원 Controller"
tags: [ spring, controller ]
date: 2019-09-19
categories: [ spring ]
---

<p align="center">
    Spring에서 지원해주는 MVC패턴 구현의 지원으로 패턴구현을 좀 더 쉽게 해보자.
</p><br/>

## ◆ SPRING - WEB
스프링에서는 MVC를 지원하기 위해 <font color="orange">DispatcherServlet</font>서블릿 객체가 전반적인 제어와 컨트롤러를 작동시켜주는 역할을 한다.

기본적으로 WEB-INF디렉터리는 접근이 불가능 하지만, Spring Contoller을 이용하면 <font color="orange">jsp파일을 WEB-INF내부에 설계</font> 해두고 직접적인 접근은 제한시키고 컨트롤러를 통해 접근되는 보안이 좀 더 향상된 형태로 작동된다.

<br/>

### ▶ 메이븐 추가 설정
- Spring Web MVC
: {% highlight ruby %}
<!-- https://mvnrepository.com/artifact/org.springframework/spring-webmvc -->
<dependency>
<groupId>org.springframework</groupId>
<artifactId>spring-webmvc</artifactId>
<version>4.3.14.RELEASE</version>
</dependency>
{% endhighlight %}

- JSP API
: {% highlight ruby %}
<!-- https://mvnrepository.com/artifact/javax.servlet.jsp/javax.servlet.jsp-api -->
<dependency>
<groupId>javax.servlet.jsp</groupId>
<artifactId>javax.servlet.jsp-api</artifactId>
<version>2.3.1</version>
<scope>provided</scope>
</dependency>
{% endhighlight %}

- Servlet API
: {% highlight ruby %}
<!-- https://mvnrepository.com/artifact/javax.servlet/javax.servlet-api -->
<dependency>
<groupId>javax.servlet</groupId>
<artifactId>javax.servlet-api</artifactId>
<version>3.1.0</version>
<scope>provided</scope>
</dependency>
{% endhighlight %}

<br/>

### ▶ web.xml 수정

<br/>

#### ※ DispatcherServlet 등록  
&nbsp;<font color="orange">WEB-INF/web.xml파일에서 DispatcherServlet을 기본 설정과 동시에 등록</font>해 주어야 한다.<br/>
자동완성(ctrl + spaceba) 기능으로 rspringDispatcherServlet을 선택하면 아래의 내용이 추가된다.
{% highlight ruby %}
<servlet>
    <servlet-name>springDispatcherServlet</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    <init-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>/WEB-INF/spring-config.xml</param-value>
    </init-param>
    <load-on-startup>1</load-on-startup>
</servlet>

<servlet-mapping>
    <servlet-name>springDispatcherServlet</servlet-name>
    <url-pattern>/</url-pattern>
</servlet-mapping>
{% endhighlight %}

- IOC컨테이너 경로 설정 
: <font color="orange">contextConfigLocation</font>의 value값으로 spring bean configuration File의 경로를 잡아준다.<br/>
기존에 ApplicationContext객체를 통해 받아오던 방식과 달리 서버가 실행됨과 동시에 IOC의 싱글톤객체들이 생성된다.
( Spring에서 설정파일등은 보통 WEB-INF디렉토리에 등록시켜 둔다. )

> contextConfigLocation의 값은 '/WEB-INF/springDispatcherServlet-servlet.xml'라는 값을 디폴트로 가지고 있기 때문에, 해당경로아래 해당파일명으로 만들 시 이를 설정해 주지 않아도 된다.

<br/>

- DispatcherServlet이 처리할 파일 경로 설정 
: <font color="orange">&lt;url-pattern>태그로 DispatcherServlet이 처리할 경로 값을 / 로 설정</font>해준다.<br/>

> 기본적으로 톰캣에서는 .jsp로 끝나는 모든 파일들을 JspServlet이 처리하도록 설정되어 있고, 디폴트로 모든 경로(/)도 JspServlet이 처리하도록 되어있기 때문에 아무 처리도 하지 않게 되면 모든 경로를 JspServlet이 처리한다.<br/>
<br/>따라서, <font color="orange">DispatcherServlet의 처리경로를 /*로 하게 되면 JspServlet이 jsp파일을 처리하지 못하기 때문에 / 로 설정해두면 jsp를 제외한 모든 문서들을 DispatcherServlet이 처리</font>하게 된다. 

springDispatcherServlet를 설정하지 않으면 스프링이 작동되지 않는다.<br/>
JspServlet이 처리하는 경로들은 서버의 web.xml 파일에 등록되어 있으므로 확인이 가능하다. <br/>단, DispatcherServlet이 처리할 경로를 등록하면 자동적으로 <font color="orange">JspServlet가 처리할 경로와 겹치는 경로들은 DispatcherSevlet이 처리</font>하도록 되어있기 때문에 서버의 web.xml파일을 수정할 필요는 없다.

<br/>

- 스프링에서는 설정들이 바로바로 잡히지 않는 경우도 많기 때문에 일단 에러가 뜰 경우 alt + f5 로 convert시키고 다시 확인

<br/>

## ◆ 핸들러(컨트롤러) 설계 ( Annotation기반 )
스프링의 컨트롤러를 설정에 있어 매핑 하는 방법에는 다양한 방식이 있다.
- BeanNameUrlHandlerMapping 
- ControllerBeanNameHandlerMapping 
- ControllerClassNameHandlerMapping, SimpleUrlHandlerMapping
- DefaultAnnotationHandlerMapping
<br/>
등이 있지만, <font color="orange">현재는 거의 다 쓰이지 않고 DefaultAnnotationHandlerMapping만 사용</font>한다.<br/>
( 스프링에서의 모든 요청은 컨트롤러로 보내고 난 후 처리되도록 설계한다. )

<br/>

### ▶ 이전 방식 컨트롤러 매핑방법
이전 방식에서는 IOC컨테이너에 매핑방식에 따른 매핑클래스를 등록해 두고 해당 방법에 따른 클래스를 상속받아 오버라이드메서드를 작성하는 방식으로 컨트롤러를 만들어 사용되었다.<br/>
또한 매핑 방식에 따라 컨트롤러를 작성하는 방식도 달랐기 때문에 설계가 매우 번거로웠을 것이다.

- ex) BeanNameUrlHandlerMapping 매핑클래스 등록예시
: {% highlight ruby %}
<bean 
class="org.springframework.web.servlet.handler.BeanNameUrlHandlerMapping"/>
{% endhighlight %}

<br/>

### ▶ DefaultAnnotationHandlerMapping 컨트롤러 매핑방법
하지만 현재는 DefaultAnnotationHandlerMapping만 쓰고 있다.<br/>
해당 매핑은 IOC컨테이너에 매핑클래스는 등록하지 않아도 자동으로 등록이 되기 때문에 <font color="orange">컨트롤러만 만들어서 IOC에 등록</font>시켜두기만 하면된다.

<br/>

### ▶ 컨트롤러 작성법
클래스파일을 만들어 두고 클래스위에 <font color="orange">@Controller을 써주면 컨트롤러로 처리</font>가 되고,<br/>
접근할 때의 호출될 메서드를 하나 만들고 그 위에 <font color="orange">@RequestMapping("접근 할 경로")를 적어 주면 컨트롤러의 접근 경로</font>가 된다.
{% highlight ruby %}
@Controller
public class HelloController {
    @RequestMapping("/hello")
    public String exec() {
        System.out.println("HelloController.exec() ");
        return "index.jsp";
    }
}
{% endhighlight %}
/hello로 접근하게 되면 해당 컨트롤러가 실행된다.

- 컨트롤러 작성 후 <font color="orange">컨트롤러 클래스를 IOC컨테이너에 등록</font>해야 인식된다.
- 이동 경로를 <font color="orange">문자열로 리턴하게 되면 해당 경로로 포워딩</font>된다.

<br/>

### ▶ 컨트롤러 매개변수 설정방법
컨트롤러 메서드에 <font color="orange">인자로 Map객체(Map map)</font>를 받게 되면 DispatcherServlet이 호출 시킬 때 Map을 생성하여 넘겨주게 된다.<br/>
이 매개 <font color="orange">인자로 들어온 Map객체를 이용하여 데이터를 put하게 되면 이동되는 페이지에서 request.getAttribute()</font>로 받아올 수 있다.<br/>
{% highlight ruby %}
// 컨트롤러
@Controller
public class HelloController {
    @RequestMapping("/hello")
    public String exec(Map map) {
        map.put("data","테스트");
        return "index.jsp";
    }
}

// 뷰
<%= request.getAttribute("data") %>
{% endhighlight %}

<br/>

> 클래스를 상속받아서 컨트롤러를 작성하는 다른 매핑 방식과 달리 Annotation매핑기반의 컨트롤러는 정해진 형식의 메서드가 없기 때문에 여러 가지 형태로 메서드를 만들 수 있는 장점이 있지만, 혼란을 줄 수 도 있다.



<br/>