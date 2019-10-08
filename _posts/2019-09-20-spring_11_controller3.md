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

- Gson/JSON ?
: <a href="/javascript/2019/05/25/javascript_5_ajax.html">Gson라이브러리 사용법</a>

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
ex ) href=“/chap04/~” <br/>

- JSP에서 루트패스 가져오기
: 프로젝트의 루트 패스를 잊어버렸거나, 수정되었을 때 해당 부분의 경로를 모두 바꾸는것이 매우 번거롭기 때문에 <font color="orange">application.getContextPath()</font>를 이용하면 ip를제외한 <font color="orange">프로젝트 루트경로를 반환</font>할 수 있다.
<br/
ex) 루트패스가 test일 때
{% highlight ruby %}
<%=application.getContextPath() %>
// =>  /test 를반환
{% endhighlight %}

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
컨트롤러를 등록할 때 IOC에 &lt;bean>태그를 이용하여 등록하여도 되지만, 컨트롤러가 많아질 경우 번거로운 작업이 될 수 있으므로 컨트롤러를 패키지로 묶어 등록시켜주는 태그가 있다. 

<br/>

### ▶ 자동 등록방법
컨트롤러를 작성할 때 하나의 패키지에 모아서 작성한다.<br/>
IOC컨테이너의 <font color="orange">Namespaces탭에서 context를 체크</font>하고 <font color="orange">&lt;context:component-scan> 태그를 사용하여 base-package옵션으로 컨트롤러가 있는 패키지를 지정</font>한다.
{% highlight ruby %}
<context:component-scan base-package="mvc.controller.study">
</context:component-scan>
{% endhighlight %}
컨트롤러에는 @Controller 어노테이션이 반드시 붙어 있어야 한다.<br/>

> 해당 방법으로 컨트롤러 뿐만 아니라 모든 클래스등록이 가능하기 때문에, 서비스(모델)객체 또한 해당 방법을 통해 등록하면 된다.

<br/>

### ▶ 서비스(모델)객체 / 자동 객체 주입
MVC패턴의 모델 또는 서비스(모델과 약간의 차이가 있음)객체를 설계할 때에도 컨트롤러와 마찬가지로 어노테이션을 지원하며, 보통 컨트롤러에서 주입(DI)받아 사용한다.<br/>

#### ▶ Service객체 설계 등록
- 1) 서비스객체를 만들고 <font color="orange">@Service</font>라는 어노테이션을 붙인다. 
: @Controller처럼 서비스객체라는 것을 인식시켜주기 위한 어노테이션으로,  @Service어노테이션이 있어야 IOC에 등록이 된다.
- 2) IOC에 패키지 등록
: &lt;context:component-scan>를 이용하여 컨트롤러와 마찬가지로 패킨지로 모아 등록시킨다.
- 3) 해당 서비스객체를 컨트롤러의 필드로 선언하고 <font color="orange">@Autowired</font> 라는 어노테이션을 붙인다.
: 기존에 ApplicationContext객체를 통해 불러오던 방식과 달리 <font color="orange">@Autowired 어노테이션만으로 타입과 일치하는 서비스객체를 주입</font>받을 수 있다. 해당 객체가 싱글톤일시 모든 클라이언트와 공유될 수 있는 객체가 된다.<br/>

<b>기존방식</b>
{% highlight ruby %}
ApplicationContext ctx =
new ClassPathXmlApplicationContext("spring/alpha/alpha-config.xml");
ctx.getBean("id");
{% endhighlight %}
<b>어노테이션방식</b>
{% highlight ruby %}
@Controller
public class Test(){
    @Autowired
    TestService ts;
}
{% endhighlight %}

<br/>

※ 등록된 컨트롤러 확인 
: 이클립스 왼쪽의 Spring Elements - Beans - Controller 에서 확인할 수 있다.

<br/>

## ◆ 스프링 필터 설정
원래의 POST방식에서는 request.setCharacterEncoding("UTF-8");를 이용하여 한글처리를 해 주어야 한다.<br/> <font color="hotpink">Spring에서 요청은 DispatcherServlet이 Controller로 넘겨</font>주는데, 해당 한글처리는 DispatcherServlet으로 요청이 넘어가기 전에 처리를 해야하지만 이것을 처리할 타이밍이 없다.<br/>
때문에 해당 타이밍에 필터를 적용하여 처리해야 하는데 다행스럽게도 <font color="orange">스프링에서는 이런 한글처리에대한 필터를 제공</font>해 주기 때문에 web.xml에 해당 필터설정만 해 주면 된다.<br/>
( 필터의 <font color="hotpink">작동 시기는 요청 후 DispacherServlet으로 넘어가기 전</font> )

<br/>

### ▶ 스프링 필터 설정법
web.xml
{% highlight ruby %}
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
{% endhighlight %}

<br/>

## ◆ 경로 자동 설정
IOC컨테이너에 스프링에서 지원하는 <font color="orange">InternalResourceViewResolver</font>객체는 컨트롤러에서 <font color="orange">포워딩하는 경로</font>에 대해 같은 경로 또는 같은 확장자를 가진 파일들의 중복처리를 일일이 쓰지 않아도 자동적으로 붙여주는 객체이다.<br/>
(단, redirect: 로 보낼시에는 적용되지 않는다. )
{% highlight ruby %}
<!-- ViewResolve -->
<bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
    <property name="prefix" value="/WEB-INF/view"></property>
    <property name="suffix" value=".jsp"></property>
</bean>
{% endhighlight %}
- prefix의 value로 설정된 값은 컨트롤러 메서드에서 반환하는 경로에 앞에 자동으로 붙도록 처리된다.
- suffix의 value로 설정된 값은 컨트롤러 메서드에서 반환하는 경로 맨 뒤에 자동으로 붙도록 처리된다.
- 위 처럼 설정할 시 컨트롤러에서 포워딩하는 경로 처리는 "/WEB-INF/view/컨트롤러반환스트링.jsp"로 처리된다.<br/>
ex) "/test"를 리턴했을 시 /WEB-INF/view/test.jsp 페이지로 포워딩!

<br/>

## ◆ 그 외
- 컨트롤러 어노테이션에 @Controller("id")의 형식으로 &lt;context:component-scan>로 등록되는 <font color="orange">컨트롤러들의 Id를 지정</font>해 줄 수 있다.<br/>

&lt;context:component-scan>로 등록된 객체들은 자동적으로 클래스이름(또는 앞에만 소문자)으로  id가 자동등록 된다.
( 일반적으로는 앞에만 소문자로 바뀌지만, 대문자가 두 개 이상 연속해서 있을 때는 그냥 클래스이름을 아이디로 사용 )
<br/><br/>
- WebContent아래에 있는 경로들은 src와 인식이 조금 다르기 때문에 xml파일을 찾을 때 꼭 classpath: 로 시작할 필요는 없다.
<br/><br/>
- spring의 트랜잭션 처리는 익셉션이 발생해야 처리되기 때문에, <font color="orange">트랜잭션을 처리</font>하는 메서드에서는 try~catch가 아닌 <font color="orange">thorw</font>로 던져야한다.
<br/><br/>
- 스프링에서는 jsp를 제외한 모든 파일들을 DispatcherServlet이 관리하기 때문에 &lt;img>태그의 src또한 DispatcherServlet이 처리한다.<br/>
하지만 <font color="orange">DispatcherServlet은 이미지파일을 처리할 수 없다.</font> 그래서 스프링설정파일(IOC컨테이너)에 아래코드를 등록시켜주면 디폴트 서블릿이 처리할 수 있도록 해준다.
{% highlight ruby %}
<mvc:annotation-driven /> 
<mvc:default-servlet-handler />
{% endhighlight %}
<br/>
- 컨트롤러에서 "redirect:/경로"와 같이 <font color="orange">redirect:키워드를 붙여서 리턴하게 되면 포워딩이 아닌 리다이렉트</font> 시킬 수 있다. 리다이렉트와 포워딩의 차이는 포워딩 시에는 포워딩된 페이지의 경로가 보이지 않는다는 것이다.<br/>

> 또한 리다이렉트시에도 Model, Map등의 객체로 파라미터를 넘길 수 있다. 하지만, <font color="orange">리다이렉트 시에는 URL을 통해 데이터를 넘겨주기 때문에</font> request.getAttribute()메서드가 아닌 <font color="orange">request.getParameter() 또는 @RequestParam 으로 받아야 한다.</font><br/>
즉 "redirect:/경로?변수=변수값"의 형식으로 리턴이 가능하며, Map이나 Model객체를 이용해 파라미터를 설정하여도 똑같은 형식으로 보내진다.

- 컨트롤러의 접근경로를 / 로 할 때는 "/index","/" 두 가지로 해야 한다.
<br/><br/>
- 컨트롤러 메서드 위에 @PostConstruct 어노테이션을 붙이게 되면 컨트롤러 초기 이닛메서드로 작동된다.







<br/>