---
layout: post
title: "11. MVC패턴 구현 지원 Controller-3"
tags: [ spring, controller ]
date: 2019-09-20
categories: [ spring ]
---

<p align="center">
    Spring Controller의 다양한 기능들을 좀 더 알아보자.
</p><br/>

## ◆ 컨트롤러의 리턴 벨류

### ▶ @ResponseBody
컨트롤러 메서드위에 @ReponseBody를 붙이게 되면 <font color="orange">리턴되는 String값은 이동될 페이지가 아닌 웹 브라우저에 출력할 String</font>이 된다. 따라서 Gson객체와 함께 <font color="orange">AJAX처리에 주로 사용</font>된다.

<br/>

#### ※ @ResponseBody 한글인식처리
- @ResponseBody로 처리할 경우 디폴트 컨텐츠 타입은 text/plain; charset=ISO-8859-1 이기 때문에 한글도 인식이 되지 않을뿐더러 JQuery에서 받아올 시 객체로 인식될 수 없다. 때문에 해당 컨텐츠타입을 바꾸어 줘야한다.
{% highlight ruby %}
@RequestMapping(path = "/03", produces = "application/json;charset=utf-8")
// @RequestMapping의 produces옵션으로 컨텐츠 타입을 바꿀 수 있다.
{% endhighlight %}

<br/>

- Spring 3.1버전 이상부터는 IOC컨테이너에 아래의 설정이 추가적으로 더 필요하게 되었다.
{% highlight ruby %}
<!-- @ResponseBody로 String 처리할때 한글처리 -->
<mvc:annotation-driven>
	<mvc:message-converters>
		<bean
class="org.springframework.http.converter.StringHttpMessageConverter">
            <property name="supportedMediaTypes">
                <list>
                    <value>text/html;charset=UTF-8</value>
                </list>
            </property>
		</bean>
	</mvc:message-converters>
</mvc:annotation-driven>
{% endhighlight %}


<br/>

### ▶ ModelAndView
Spring초창기에 사용하던 리턴 타입으로, 컨트롤러 메서드에서 포워딩할 경로와 넘겨줄 데이터를 같이 설정하여 리턴하게되는 객체이다. 하지만 <font color="orange">어노테이션 형태의 컨트롤러가 지원되면서 자주 쓰이지는 않지</font>만 종종 사용하는 형태의 리턴타입이다. 

1. 컨트롤러 메서드에 ModelAndView객체를 생성
2. setVewName( 경로 ) : 해당 메서드로 포워딩할 경로를 설정한다.
3. addObject( "키", "벨류") : 해당 메서드로 넘겨줄 데이터를 설정한다.
4. 생성 및 설정해둔 ModelAndView객체를 리턴 한다.
{% highlight ruby %} 
@RequestMapping("/04")
public ModelAndView junior04Handle() {
    ModelAndView mav = new ModelAndView();
    mav.setViewName("/WEB-INF/view/index.jsp");  // 이동경로
    mav.addObject("msg", "ModelAndView 리턴");  // 넘겨줄 데이터
    mav.addObject("data", "Model,View,Contoller".split(","));
    return mav;
}
{% endhighlight %}
addObject()로 설정한 데이터들은 똑같이 request.getAttribute()로 받을 수 있다.

<br/>

## ◆ 스프링 경로처리

### ▶ 절대경로
페이지의 접근 경로는 <font color="orange">웹에서 인식하는 경로(WebContent)와 자바클래스(javaResource)에서 인식하는 루트경로가 다르다.</font><br/>
프로젝트의 접근 루트경로를 ‘/’ 가 아닌 다른 이름(ex) ‘/chap04’ )으로 설정해 놓았을 때,

- 웹 브라우저(WebContent) 
: <font color="orange">루트를 ip까지만 인식</font>하고 수정한 루트를 루트로 인식하지 못하기 때문에
절대경로를 적어줄 경우, 수정한 루트경로부터 적어주어야 한다.<br/>
ex ) href=“/chap04/~” 

- 자바클래스(JavaResource)
: <font color="orange">자바 클래스(컨트롤러 등)에서는 수정한 루트를 루트로 인식</font>하기 때문에 절대경로를 적을 때 수정한 경로까지 적어줄 필요는 없다. <br/>
※ 컨트롤러에서 @RequestMapping("/eta/04")로 설정했다면 html에서 a태그등으로 컨트롤러의 경로를 연결할 때에는 "프로젝트경로/eta/04"로 접근해야 한다.

> 프로젝트 접근 경로를 "/"로 설정했을 경우에는 루트경로에 대해 신경쓸 필요는 없다.

<br/>

### ▶ 상대경로
컨트롤러로 이용하여 처리하는 경우 포워딩을 이용하여 페이지를 이동시키기 때문에 주소창에 해당 jsp파일 경로가 나오지 않게 된다.<br/>
따라서 포워딩으로 이동했을 때, 해당 <font color="hotpink">jsp파일이 보여질 지라도 해당경로는 컨트롤러의 RequestMapping경로</font>이다. 
<br/><br/>
즉, /a 라는 컨트롤러 경로를 통해 접근했을 때, a href="b/c"의 이동 경로는 /a/b/c 이다.

<br/>

## ◆ 컨트롤러 자동 등록방법
: 컨트롤러를 등록할 때 <bean>태그를 이용하여 등록하여도 되지만,
컨트롤러를 자동으로 인식해서 등록시켜주는 태그가 있다. 

▶ 자동 등록방법
: IOC컨테이너의 Namespaces탭에서 context를 체크하고
<context:component-scan> 태그를 사용하여 base-package옵션으로 컨트롤러가 있는 
패키지를 지정한다.
ex )
<context:component-scan
 base-package="mvc.controller.study"></context:component-scan>
=> 어노테이션( @ )이 붙어있는 컨트롤러등의 객체를 알아서 인식하여 등록시켜 준다.
따라서 컨트롤러를 만들 때 마다 <bean>을 이용하여 등록시킬 필요 없이, 패키지에 컨트롤러를 모아두고 설정을 잡아두면 된다.

▶ 컨트롤러안의 개체(서비스) 등록방법
: 컨트롤러 안에 선언된 객체 또한 주입받아서 사용해야 하는데, 
해당 객체를 불러올 타이밍이 업기 때문에
똑같이  <context:component-scan >태그를 이용하여 자동 등록되게 해준다.
1. 서비스객체를 만들고 @Service 라는 어노테이션을 붙인다. 
2. 해당 서비스객체를 컨트롤러의 필드로 선언하고 @Autowired 라는 어노테이션을 붙인다.
3. 설정파일에서 똑같이 서비스클래스가 있는 패키지를 설정하여 등록하면 된다.
※ 등록된 컨트롤러 확인 
: 이클립스 왼쪽의 Spring Elements - Beans - Controller 에서 확인할 수 있다.

◆ 스프링 필터 설정
: 원래의 POST방식에서는 request.setCharacterEncoding("UTF-8");를 이용하여 한글처리를 해 주어야 하지만, 
스프링에서는 컨트롤러로 처리하게 될 경우 이것을 DispacherServlet으로 넘기기 전에 처리해야 하는데, 이것을 처리할 타이밍이 없기 때문에 필터로 캐릭터인코딩을 설정해서 보내야 한다.
하지만, 스프링에서는 이 한글처리에 대한 처리를 해주는 필터링이 등록되어 있기 때문에 해당 필터를 web.xml에 등록만 시켜주면 된다.
( 필터의 작동 시기는 요청 후 DispacherServlet으로 넘어가기 전 )

▶ 스프링 필터 설정법
web.xml
<!-- request encodng filter register -->
<filter>
<filter-name>encodingFilter</filter-name>
<filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
<init-param>
<param-name>encoding</param-name>
<param-value>utf-8</param-value>
</init-param>
</filter>
<filter-mapping>
<filter-name>encodingFilter</filter-name>
<url-pattern>/*</url-pattern>
</filter-mapping>

◆ 경로 자동 설정
: IOC컨테이너에 스프링에서 지원하는 InternalResourceViewResolver객체는 컨트롤러에서 포워딩하는 경로에 대해 같은 경로 또는 같은 확장자를 가진 파일들의 중복처리를 일일이 쓰지 않아도 자동적으로 붙여주는 객체이다.
(단, redirect: 로 보낼시에는 적용되지 않는다. )
ex )
<!-- ViewResolve -->
<bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
<property name="prefix" value="/WEB-INF/view"></property>
<property name="suffix" value=".jsp"></property>
</bean>
- prefix의 value로 설정된 스트링은 컨트롤러 메서드에서 반환하는 경로에 앞에 붙도록 자동 처리되고,
- suffix의 value로 설정된 스트링은 컨트롤러 메서드에서 반환하는 경로 맨 뒤에 붙도록 자동 처리된다.
=> prefix는 앞의 경로를 설정 하는 용도, suffix는 뒤의 확장자를 설정하는 용도.

◆ 그 외
▶ @Controller("id")의 형식으로 <context:component-scan>으로 등록되는 컨트롤러의 Id를 지정해 줄 수도 있다.
▶ <context:component-scan>으로 등록된 객체들은 자동적으로 클래스이름(또는 앞에만 소문자)으로  id가 자동등록 된다.
( 일반적으로는 앞에만 소문자로 바뀌지만, 대문자가 두 개 이상 연속해서 있을 때는 그냥 클래스이름을 아이디로 사용 )
▶ WebContent아래에 있는 경로들은 src와 인식이 조금 다르기 때문에 xml파일을 찾을 때
꼭 classpath: 로 시작할 필요는 없다.
▶ 트랜잭션 처리는 익셉션이 발생해야 처리되기 때문에, 트랜잭션을 처리하는 메서드에서는 트라이캐치가 아닌 thorw로 던져야한다.
▶ 스프링에서는 jsp를 제외한 모든 파일들을 DispatcherServlet이 관리하기 때문에
<img>태그의 src또한 DispatcherServlet이 처리한다.
하지만 DispatcherServlet은 이미지파일을 처리할 수 없기 때문에 스프링설정파일(IOC컨테이너)에
<mvc:annotation-driven /> 
<mvc:default-servlet-handler /> 
를 등록시켜주면 디폴트 서블릿이 처리할 수 있도록 해준다.
▶ 컨트롤러 메서드에서 "redirect:/경로"를 리턴하게 되면 페이지를 리다이렉트 시킬 수도 있다.
리다이렉트와 포워딩의 차이는 포워딩은 경로가 보이지 않는다.
=> 리다이렉트 또한 Model등의 객체로 파라미터를 설정할 수 이으며, 리다이렉트의 경우에는 request.getAttribute()메서드가 아닌
request.getParameter() 또는 @RequestParam 으로 받아야 한다.
또한 "redirect:/경로?변수=변수값" 등으로 파라미터를 보낼 수도 있다.
▶ 컨트롤러의 접근경로를 / 로 할 때는 "/index","/" 두 가지로 해야 한다.
▶ 컨트롤러 메서드 위에 @PostConstruct 어노테이션을 붙이게 되면 컨트롤러 초기 이닛메서드로 작동된다.







<br/>