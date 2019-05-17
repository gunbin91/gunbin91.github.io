---
layout: post
title: "3. 서블릿(Servlet)"
tags: [ jsp, servlet ]
date: 2019-05-14
categories: [ jsp ]
---

<p align="center">
    JSP로 작성한 코드는 서블릿이란 자바코드로 변환되어 서버에 등록된다. 웹 페이지는 서블릿으로도, jsp로도 작성할 수 있기 때문에 둘 다 알아두는 것이 좋다.
</p><br/>

# ◆ 데이터 전달
서블릿을 만들기 전 웹에서는 데이터를 어떤식으로 전달하는지 알아보자. 웹에서 클라이언트가 데이터를 보내는 형식은 정해져있다. 
<br/>

#### ▶ Get방식의 QueryString
Get방식은 Url을 통해 데이터를 전달하는 접근 방식이며 목적지 뒤에 '?이름 =값'형식으로 보내며, 이런 데이터 전달 스트링을 QueryString이라고 부른다.<br/> 
<b>ex) localhost:80/home.jsp<font color="orange">?name=gb</font></b><br/>

<br/>

#### ▶ 데이터가 여러개 일 때
데이터가 여러개일 때는 구분자로 &를 붙인다.<br/>
<b>ex ) localhost:80/home.jsp<font color="orange">?id=gb&pass=1234</font></b>

<br/>

#### ▶ 데이터 불러오기
클라이언트로부터 전달받는 값들은 request객체를 통해서 확보할 수 있다.<br/>
request.getParameter()메서드의 인자로 보낸 데이터의 이름을 주면, 이름에 해당하는 값을 돌려준다.<br/>
ex) request.getParameter(“id”);

<br/>

# ◆ Servlet 만들기 ( 기본 작업은 생성자에서 하게 된다. )

<b style="color:hotpink">1. 일반클래스에 GenericServlet 또는 HttpServlet을 extends(상속)시켜서 만든다.</b>
<br/>
( Servlet(인터페이스) <- GenericServlet(추상클래스) <- HttpServlet 의 상속 구조 )
<br/>

> 이 과정에서 WAS에서 제공하는 라이브러리가 필요하다<br/>
WAS설치폴더(톰캣)/lib/jsp-api.jar, servlet-api.jar를<br/>
프로젝트/WEB-INF/lib 로 복사해서 라이브러리 추가를 해준다.<br/>
( lib파일에 추가 할 시 Libraries/Web app Libaries 아래에 똑같이 라이브러리가 추가 된다. )

#### 1-2 new를 이용하여 쉽게 서블릿 만들기
프로젝트우클릭 -> new -> Servlet<br/>
해당 서블릿의 경로를 미리 설정해 둘 수 있고 doGet(), doPost()등의 메서드를 자동으로 작성되도록 체크할 수도 있다.<br/>

- doGet()
: 클라이언트의 접근 method가 GET방식일 때 호출되는 메서드로 <font color="orange">URL값으로 정보가 전송</font>되기 때문에 보안에 취약하다.

- doPost()
: 클라이언트의 접근 method가 POST방식일 때 호출되는 메서드로 <font color="orange">header를 통해 정보가 전달되기 때문에 보안에 강하고, URL로 데이터가 노출되지 않는다.</font>

> URL을 직접입력 할 경우 또는 form태그의 method속성이 GET일 때 GET방식으로 접근이 되고, form태그의 method속성이 POST일 때 POST방식으로 접근된다.

<br/>

<b style="color:hotpink;">2. 서블릿 매핑작업</b><br/>
서블릿을 만들고 해당 서블릿으로 접근될 경로를 지정해 주어야 한다. 서블릿의 경로를 매핑하는 방법에는 두 가지가 있다.

#### ▶ 2-1 WEB-INF/web.xml에 서블릿 등록과 매핑작업

- 서블릿 등록
: 서블릿을 등록할 때 서블릿 클래스경로는 /가 아닌 .으로 지정한다.<br/>
ex) &lt;servlet-class>pac.one.servlet1&lt;/servlet-class>
{% highlight ruby %}
<servlet>
    <servlet-name> 아무이름 </servlet-name>
    <servlet-class> 작성한 클래스 </servlet-class> 
<servlet>
 {% endhighlight %}
- 서블릿 매핑
: 경로를 매핑할 때는 서블릿을 등록할 때 &lt;servlet-name>태그로 등록한 이름으로 매핑한다.
{% highlight ruby %}
<servlet-mapping>
    <servlet-name> 위에서 작성한 이름 </servlet-name>
    <url-pattern> 주소창에 등록할 경로 </url-pattern> // 반드시 슬래시(/)로 시작
</servlet-mapping>
{% endhighlight %}

> 모든 web.xml의 설정들은 미리 지정되어 있는 &lt;web-app>태그 안에서 해준다.

<br/>

#### ▶ 2-2 어노테이션을 이용한 서블릿 등록과 매핑
서블릿 클래스 위에 <font color="orange">@WebServlet("/경로")</font>를 적어주게 되면 web.xml에 등록하지 않고도 서블릿의 등록과 매핑이 한번에 해당 경로로 설정이 된다.<br/>
JAVA에서 <font color="orange">@로 지정하는 설정들을 어노테이션</font>이라고 한다.
{% highlight ruby %}
@WebServlet("/test")
public class test extends HttpServlet {
	private static final long serialVersionUID = 1L;
    
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		response.setCharacterEncoding("utf-8");
		response.setContentType("text/html"); 
		PrintWriter out = response.getWriter();
		out.println("<html><head></head><body><h1>GET접근</h1></body></html>");
	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		doGet(request, response);
	}
}
{% endhighlight %}

> 주의해야 할 점은 web.xml과 어노테이션을 이용하여 동시에 매핑이 가능하다는 점인데, 동시에 매핑할 경우 기능은 같지만 서로 다른 서블릿 객체라고 봐야한다.

<br/>

# ◆ 서블릿 초기 값 만들기
web.xml에서 특정 서블릿의 초기값을 만들 수 있다. 서블릿 초기값 설정도 경로 매핑과 마찬가지로 두 가지의 방법이 있다.

<br/>

#### 1. web.xml에서 초기값 설정
서블릿 매핑작업 시 등록할 때 사용한 <servlet>태그 안에서 초기값 들을 설정할 수 있다.
{% highlight ruby %}
<servlet>
    <init-param>
        <param-name> 변수명 </param-name>
        <param-value> 값 </param-value>
    <init-param>

    <init-param>
        <param-name> 변수명 </param-name>
        <param-value> 값 </param-value>
    <init-param>
…
</servlet>
{% endhighlight%}

<br/>

#### 2. 어노테이션을 이용한 초기값 설정
어노테이션을 이용할 때 마찬가지로 매핑시 사용했던 @WebServlet안에서 지정한다.<br/>
단, 이렇게 지정할 경우 기존에 어노테이션으로 지정한 경로매핑이 있다면 아래와 같이 바꿔주어야 한다.<br/>
{% highlight ruby %}
@WebServlet(
    urlPatterns = {"/test"}, 
    initParams = {
        @WebInitParam(name="id", value="ano"), 
        @WebInitParam(name="pass", value="111")
    }
)
{% endhighlight %}

<br/>

#### ▶ 서블릿 초기값 뽑아내기
서블릿 최초접근 시 호출되는 init()메서드에 있는 인자인 ServletConfig config객체의 메서드인 getInitParameter()메서드로 초기값을 뽑아내어 작업 할 수 있다.<br/>
ServletConfig객체는 상속받은 것이기 때문에 꼭 인자가 없어도 변수명 없이 사용이 가능하다.<br/>
따라서, <font color="orange">getInitParameter("설정변수")메서드 만으로 서블릿의 초기값을 String형으로 뽑아낼 수 있다.</font>
{% highlight ruby %}
protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		response.setCharacterEncoding("utf-8");
		response.setContentType("text/html"); 
		PrintWriter out = response.getWriter();
		out.println("<h1>서블릿 초기값 : </h1>" + getInitParameter("id"));
}
{% endhighlight %}

> 단, 서블릿 매핑 시 web.xml과 어노테이션의 두 가지 방법이 있듯이, 동시에 처리하게 될 경우 <font color="orange">web.xml에서 설정한 초기값은 web.xml에서 매핑한 경로에서만 적용되고, 어노테이션으로 등록한 초기값은 어노테이션에서 설정한 경로에서만 적용된</font>다. 따라서 이를 이용하여 초기값이 다른 두개의 같은 페이지를 만들 수도 있다.

<br/>

# ◆ Context(공통) 초기 값 만들기
서블릿 초기값은 ServletConfig객체에서 뽑아 내어 하나의 서블릿 안에서만 적용 되었지만, ServletConfig객체에서 뽑아낼 수 있는 <font color="orange">ServletContext객체에 등록된 초기값은 여러 서블릿에서 공유할 수 있는 초기값을 설정</font>하는 것이다.

<br/>

#### ▶ Context초기값 설정
web.xml에서 지정하며, 특정 서블릿에서 사용하는 값이 아니기 때문에 어노테이션을 이용하는 방법은 없고, 어떤 식으로 매핑하던 같은 값을 공유한다.
{% highlight ruby %}
<context-param>
	<param-name>conid</param-name>
	<param-value>contextid</param-value>
</context-param>
{% endhighlight %}

<br/>

#### ▶ 호출방법
Context초기값을 뽑아내기 위해서는 ServletContext객체가 필요하다. 이 객체는 ServletConfig객체에서 뽑아낼 수 있는데, ServletConfig객체는 변수명없이 사용할 수 있기 때문에 <font color="orange">getServletContext()메서드만을 이용하여 ServletContext객체를 뽑아낼 수 있다.</font><br/>
객체를 뽑아낸 후 <font color="orange">ServletContext객체의 getInitParam("네임")메서드를 이용하여 초기값을 뽑아낸다.</font><br/>
{% highlight ruby %}
protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		response.setCharacterEncoding("utf-8");
		response.setContentType("text/html"); 
		PrintWriter out = response.getWriter();
		out.println("<h2>컨텍스트초기값</h2>");
		out.println(getServletContext().getInitParameter("conid"));
}
{% endhighlight %}

> 주의) init메서드를 오버라이드 할 때 super.init(context)를 지워버리면 ServletContext객체를 불러올 때 널포인트 익셉션이 발생할 수 있다.

<br/>

# ◆ ServletRequest 
extneds GenericServlet 또는 extends HttpServlet 클래스의 기본 오버라이드 메서드 service의 인자로 받는 <font color="hotpink">ServletRequest객체는 클라이언트에서 요청으로 받아오는 모든 데이터를 저장</font>하는 객체

<br/>

#### ▶ request 기본 메서드 
- request.getParameterMap()
: 전달받은 데이터 전체를 Map<String, String[]>으로 반환 

- String addr = request.getRemoteAddr(); 
: (클라이언트)접속된 ip (address)반환

- int port = request.getRemotePort(); 
: (클라이언트)접속된 port 반환

- Locale loc = request.getLocale();
: loc.getCountry = 사용언어 반환

- request.getParamenterNames();
: Iterator객체와 비슷한 Enumeration&lt;String> 객체를 반환하게 됨.<br/>
{% highlight ruby %}
Enumeration<String> names = request.getParameterNames();
while(names.hasMoreElements()) { // 다음 데이터가 있는지 확인
	String name = names.nextElement(); // 데이터를 반환하고 다음으로 이동
	String value = request.getParameter(name);
	out.println("네임 : " + name);
	out.println("벨류 : " + value);
}
{% endhighlight %}
- request.getParameter("이름");
: 넘어온 데이터의 이름을 알고 있는 경우 바로 스트링으로 입력하면 value값이 나온다.<br/>
( 멀티플 데이터의 경우 해당 이름에 해당하는 벨류값의 [0]인덱스의 벨류값을 반환 )
- reuqest.getParameterValues("이름");
: value값이 여러개가 넘어온 경우 String[]배열로 반환되는 메서드

<br/>

# ◆ ServletResponse
요청이 들어온 클라이언트로 보낼 응답을 담당하는 객체
<br/>

#### ▶ response 기본 메서드
- response.setCharacterEncoding("utf-8"); 
: 응답 문자셋 설정
- response.setContentType("text/html"); 
: 응답문서 종류 설정<br/>
=> response.setContentType("text/html;charset=utf-8");로 문자셋과 문서 동시처리 가능
- PrintWriter out = response.getWriter();
: 인터넷 브라우저에 출력할 out객체 ( out.println 으로 출력가능 )

<br/>

#### ▶ get방식 문자인코딩 설정방법
Server의 server.xml파일을 열어 
{% highlight ruby %}
<Connector connectionTimeout="20000" port="8181" protocol="HTTP/1.1" redirectPort="8443"/>
// 해당 부분을 아래와 같이 URIEncoding속성을 추가해준다.
<Connector URIEncoding="UTF-8" connectionTimeout="20000" port="8181" protocol="HTTP/1.1" redirectPort="8443"/>
{% endhighlight %}

> Eclipse상에서 server디렉터리는 복사본이기 때문에, 실제 경로에 적용되기 위해서는 실제 경로상의 서버디렉터리에서 수정하여야 한다.( 또는 싱크로나이즈)

<br/>









<br/>