---
layout: post
title: "15. Tiles템플릿 엔진"
tags: [ spring, tiles ]
date: 2019-10-07
categories: [ spring ]
---

<p align="center">
    
</p><br/>

## ◆ 템플릿 엔진(템플릿 프레임워크) - Tiles
일정 틀을 유지하면서 view를 꾸며야 할 때, 템플릿엔진(프레임워크)을 사용하면 쉽게 구현이 가능함.<br/>스프링에 국한된 내용이 아니라, 굳이 스프링이 아니더라도 템플릿엔진은 사용이 가능함.<br/>
- 스프링은 이 템플릿 프레임워크를 이용해서 view를 처리하는 것을 지원함
- 다양한 종류의 템플릿엔진이 이는데, 그 중에서 Tiles라는 걸 이용해서처리

<br/>

### ▶ 라이브러리 추가
<a href="https://tiles.apache.org/download.html">https://tiles.apache.org/download.html</a>로 접속하여 <font color="orange">Tiles3.0버전</font> 메이븐 3개중에 밑에 두개 받기

<br/>

### ▶ 스프링 설정파일에 추가
2버전 3버전이 있지만 3버전으로 받도록 하자
{% highlight ruby %}
<bean class="org.springframework.web.servlet.view.tiles3.TilesViewResolver"></bean>
<bean class="org.springframework.web.servlet.view.tiles3.TilesConfigurer">
    <property name="definitions">
        <array>
            <value>/WEB-INF/tiles/*-tiles.xml</value>
        </array>
    </property>
</bean>
{% endhighlight %}
definitions의 값을 array로 여러개의 tiles설정 파일을 등록할 수 있다.

<br/>

### ▶ definitions파일 만들기
위에서 설정한 경로로 해당 이름의 xml파일을 만든다.<br/> <a href="https://tiles.apache.org/framework/tutorial/basic/pages.html"> https://tiles.apache.org/framework/tutorial/basic/pages.html</a>로 접속하여 아래와 비슷한 형태를 복사해서 붙여넣어준다.
{% highlight ruby %}
<!DOCTYPE tiles-definitions PUBLIC "-//Apache Software Foundation//DTD Tiles Configuration 3.0//EN" 
"http://tiles.apache.org/dtds/tiles-config_3_0.dtd">
{% endhighlight %}

<br/>

### ▶ definitions파일 설정
위에서 만든 xml파일에서 아래와 같이 템플릿설계를 추가한다.
{% highlight ruby %}
<tiles-definitions>
    <definition name="index" template="/WEB-INF/view/mainTemplate.jsp">
        <put-attribute name="title" value="Spring MVC"></put-attribute>
        <put-attribute name="side" value="/WEB-INF/view/side-01.jsp"/>
        <put-attribute name="main" value="/WEB-INF/view/login.jsp"/>
    </definition>
</tiles-definitions>
{% endhighlight %}
- &lt;definition name="index" template="/WEB-INF/view/mainTemplate.jsp"> 
: 컨트롤러에서 <font color="orange">리턴 할 때 name에 설정한 ‘index’이름을 리턴하면 template의 경로로 이동</font>하게 된다.<br/>
- &lt;put-attribute>
: 사용되는 jsp페이지에서 문자열로 불러오거나, 해당 경로를 include하기 위해 사용하는 파라미터값

<br/>

### ▶ 컨트롤러 경로 리턴 우선순위
Tiles의 definition <font color="hotpink">name과 컨트롤러의 RequestMapping이름이 같을 때, TilesViewResolver와 InternalResourceViewResolver의 우선순위</font>에 따라 어떤 경로로 이동할 것인지 설정할 수 있다.

- TilesViewResolver설정
: {% highlight ruby %}
<bean
 class="org.springframework.web.servlet.view.tiles3.TilesViewResolver">
    <property name=“order” value=“1”> // 우선순위 1
</bean>
<bean class="org.springframework.web.servlet.view.tiles3.TilesConfigurer">
    <property name="definitions">
        <array>
            <value>/WEB-INF/tiles/*-tiles.xml</value>
        </array>
    </property>
</bean>
{% endhighlight %}


- InternalResourceViewResolver설정
: {% highlight ruby %}
<bean
class="org.springframework.web.servlet.view.InternalResourceViewResolver">
    <property name="prefix" value="/WEB-INF/view/"></property>
    <property name="suffix" value=".jsp"></property>
    <property name="order" value="2"> // 우선순위 2
</bean>
{% endhighlight %}
- InternalResourceViewResolver은 컨트롤러에서 경로를 리턴 할 때 해당 이름 앞(prefix)과 뒤(suffix)에 자동적으로 붙여질 이름을 설정하는 객체이다.
- &lt;property name="order" value="1">을 적어주어 <font color="orange">value의 숫자가 낮은 쪽이 우선순위가 높아진다.</font> 따라서 Tiles의 우선순위가 높을 경우 RequestMapping과 Tiles name이 겹치지 않을때만 prefix와suffix를 붙인 경로로 이동된다.

> 단, 주의할 점으로는 InternalResouceViewResover를 먼저 등록 시키게 되면, 페이지 낫 파운드가 발생하므로 TilesViewResolver를 먼저 등록시켜야 한다. 

<br/>

### ▶ JSP뷰 파일 만들기
definitions파일에서 설정한 template경로의 jsp파일을 만들어 <font color="orange">&lt;%@ taglib prefix="tiles" uri="http://tiles.apache.org/tags-tiles"%></font>를 추가하여 Tiles에서 제공하는 기능을 JSTL태그를 통하여 사용할 수 있도록 한다.

- &lt;tiles:<font color="orange">getAsString</font> name="title"></tiles:getAsString>
: 타일즈 설정파일에 등록한 title이라는 name의 <font color="orange">value를 문자열로 가져오기</font>

- &lt;tiles:<font color="orange">insertAttribute</font> name="side"></tiles:insertAttribute>
: 타일즈 설정파일에 등록한 side라는 name의 <font color="orange">value경로 jsp파일을 include</font>

<br/>
위 Definitions설정처럼 설정했을 시 아래와 같은 결과를 얻는다.
{% highlight ruby %}
<%@ taglib prefix="tiles" uri="http://tiles.apache.org/tags-tiles"%>

// => Spring MVC 반환
<tiles:getAsString name="title"/> 

// => /WEB-INF/view/side-01.jsp 를 include
<tiles:insertAttribute name="side">
{% endhighlight %}

> Attribute를 Definitions파일에 등록해두고 문자열이나 경로로 반환받기 때문에 해당 경로에 파일이 존재하지 않아도 불러오지 않으면 에러가 발생하지 않는다.<br/> 또한 tiles에 의해 합쳐진 jsp파일 모두에서 해당 Attribute를 사용할 수 있으며, EL태그를 통해 템플릿을 좀 더 동적으로 사용할 수 있다.

<br/>

### ▶ Tiles 중복처리
반복적으로 포함되는 일정한 패턴같은 경우는 <font color="orange">extends옵션에 포함할 name을 적어 상속받아 사용하면 일일히 추가할 필요가 없다.</font>
{% highlight ruby %}
<definition name="t_default" template="/WEB-INF/view/mainTemplate.jsp">
    <put-attribute name="title" value="Spring MVC"/>
    <put-attribute name="side" value="/WEB-INF/view/side-01.jsp"/>    
</definition>

<definition name="index" extends="t_default">
    <put-attribute name="title" value="override"/>
    <put-attribute name="main" value="/WEB-INF/view/index.jsp"/>
</definition>

// title값은 override가 된다.
{% endhighlight %}
템플릿을 상속받게 될 경우 <font color="orange">중복되는 속성은 상속받은 쪽의 값이 우선으로 덮어씌워지고, 없는 값들은 추가</font>된다.

<br/>

## ◆ Tiles EL태그 지원
tiles에서는 EL태그를 지원해 주기 때문에 좀 더 동적으로 페이지를 설계할 수 있다.<br/>
타일즈에서 <font color="orange">EL태그를 사용하기 위해서는 TILES EL SUPPORT</font> 라이브러리가 필요하다

<br/>

### ▶ 메이븐 추가
{% highlight ruby %}
<!-- https://mvnrepository.com/artifact/org.apache.tiles/tiles-el -->
<dependency>
    <groupId>org.apache.tiles</groupId>
    <artifactId>tiles-el</artifactId>
    <version>3.0.8</version>
</dependency>
{% endhighlight %}

<br/>

### ▶ 사용법
&lt;put-attribute>태그의 값을 value가 아닌 <font color="orange">expression으로 셋팅하면 EL태그의 값으로 설정</font>할 수 있다.<br/>

컨트롤러에서 <font color="orange">Map이나 Model객체를 통해 셋팅한 값을 파일명등에 셋팅시켜 동적인 페이지 변환이 가능</font>하도록 구성할 수 있고,<br/> Tiles설정파일의 등록할 개수를 최소화 시킬 수도 있다.<br/>

{% highlight ruby %}
<definition name="t_el" extends="t_default">
    <put-attribute name="main" expression="/WEB-INF/view/${main}"/>
</definition>
{% endhighlight %}
                                   
> Tiles사용 주의)<br/>
Tiles로 만들어진 페이지에서 해당 페이지를 제외한 include로 포함되는 페이지들은 &lt;head>나 &lt;body>등 공통적인 설정태그들은 모두 지워주어야 한다.<br/>
즉, 중간에 그대로 삽입된다고 생각하고 설계해야한다.





<br/>