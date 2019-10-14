---
layout: post
title: "16. Sitemesh 템플릿 엔진"
tags: [ spring, sitemesh ]
date: 2019-10-14
categories: [ spring ]
---

<p align="center">
    
</p><br/>


## ◆ Sitemesh?
Tiles와 같은 템플릿 엔진으로 뷰단의 디자인패턴을 구현하는데 사용된다.<br/>
Tiles는 Composite view패턴이라는 것을 사용하고 sitemesh는 Decorator패턴을 사용하는데,<br/>
간단히 비교하여 <font color="hotpink">Tiles는 설정이 복잡하지만 재활용성 및 성능은 우수</font>하고, <font color="hotpink">Sitemesh는 재활용성이나 성능면에서 좀 더 떨어지지만 설정이 쉽다.</font>

> http://wiki.sitemesh.org/wiki/display/sitemesh/Learn+-+Getting+Started+with+SiteMesh 에서 간단한 사용법을 확인할 수 있다.

<br/>

### ▶ 라이브러리 설치
http://wiki.sitemesh.org/wiki/display/sitemesh/Download에서 다운받아 lib디렉터리에 추가하거나 메이븐으로 설치
{% highlight ruby %}
<!-- https://mvnrepository.com/artifact/opensymphony/sitemesh -->
<dependency>
    <groupId>opensymphony</groupId>
    <artifactId>sitemesh</artifactId>
    <version>2.4.2</version>
</dependency>
{% endhighlight %}

<br/>

## ◆ Sitemesh설정


### ▶ Web.xml에 필터추가
: Sitemesh가 작동될 수 있도록 필터 매핑작업을 해준다.
{% highlight ruby %}
<filter>
  <filter-name>sitemesh</filter-name>
  <filter-class>com.opensymphony.sitemesh.webapp.SiteMeshFilter</filter-class>
</filter>
 
<filter-mapping>
  <filter-name>sitemesh</filter-name>
  <url-pattern>/*</url-pattern>
</filter-mapping>
{% endhighlight %}

<br/>

### ▶ WEB-INF 아래에 sitemesh.xml 작성
Sitemesh가 처리하는 전반적인 설정등을 작업하고, 후에 작성할 decorators.xml파일의 경로를 지정해 주어야 한다.
{% highlight ruby %}
<?xml version="1.0" encoding="UTF-8"?>
<sitemesh>
    <property name="decorators-file" value="/WEB-INF/decorators.xml" />
    <excludes file="${decorators-file}" />
 
    <page-parsers>
        <parser content-type="text/html"
            class="com.opensymphony.module.sitemesh.parser.HTMLPageParser" />
        <parser content-type="text/html;charset=UTF-8"
            class="com.opensymphony.module.sitemesh.parser.HTMLPageParser" />
    </page-parsers>
 
    <decorator-mappers>
        <!-- Mapper allows pages to specify decorator using meta tag, -->
        <!-- <meta name="decorator" content="yourDecoratorName"/> -->
        <mapper class="com.opensymphony.module.sitemesh.mapper.PageDecoratorMapper">
            <param name="property.1" value="decorator" />
            <param name="property.2" value="meta.decorator" />
        </mapper>
        
        // ★ decorators.xml파일 경로 설정
        <!-- The ConfigDecoratorMapper MUST be located after other mappers. -->
        <mapper class="com.opensymphony.module.sitemesh.mapper.ConfigDecoratorMapper">
            <param name="config" value="${decorators-file}"/>
        </mapper>
    </decorator-mappers>
</sitemesh>
{% endhighlight %}

<br/>

## ◆ Sitemesh 사용법 


### ▶ WEB-INF아래 decorators.xml 작성
Sitemesh의 레이아웃을 사용할 경로를 해당 파일에 작성한다.<br/>
(경로는 포함시킬 페이지의 경로가 아닌 컨트롤러의 접근경로를 적어준다.)

- <font color="orange">&lt;excludes></font>
: Sitemesh를 사용하지 않는 경로를 지정하는 태그
- <font color="orange">&lt;decorator></font>
: Sitemesh의 기본 레이아웃을 설정하고, 해당 레이아웃을 사용할 경로를 지정하는 태그

{% highlight ruby %}
<?xml version="1.0" encoding="UTF-8"?>  
 
<decorators defaultdir="/WEB-INF/jsp/decorators">
 
    <excludes>
      <pattern>/includeSample/*</pattern>
    </excludes>    
    
    <decorator name="sitemeshSample" page="layout.jsp">
       <pattern>/sitemeshSample/view/*</pattern>  
    </decorator>  
    
    <decorator name="sitemeshSamplePopup" page="popup.jsp">
       <pattern>/sitemeshSample/popup/*</pattern>  
    </decorator>  
    
</decorators>
{% endhighlight %}
위 처러 설정하게 되면
/includeSample/* 경로로 접근하게 되면 sitemesh를 사용하지 않게 되고,<br/>
/sitemeshSample/view/*경로로 접근하는 모든 페이지는 
/WEB-INF/jsp/decorators/layout.jsp를 기본 레이아웃으로 하는 sitemesh를 사용한다.

<br/>

### ▶ 레이아웃 작성
기본 틀이되는 레이아웃을 작성하고 해당 레이아웃 페이지에서 컨트롤러에서 리턴하는 페이지의 일부를 해당 레이아웃에서 사용할 수 있다.
- <font color="orange">&lt;decorator:head /></font> 
: 컨트롤러에서 리턴하는 페이지의 head를 불러온다.
- <font color="orange">&lt;decorator:body /></font> 
: 컨트롤러에서 리턴하는 페이지의 body를 불러온다.

{% highlight ruby %}
<?xml version="1.0" encoding="UTF-8" ?>
<%@ taglib uri="http://www.opensymphony.com/sitemesh/decorator"
	prefix="decorator"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
    <decorator:head />
    <body>
        <h1>Sitemesh Header</h1>
        <hr />
        <decorator:body />
        <hr />
        <h1>Sitemesh Footer</h1>
    </body>
</html>
{% endhighlight %}

<br/>

### ▶ &lt;decorator:getProperty>
&lt;decorator:body/>를 이용하여 불러올 때 불러오는 페이지의 body속성을 불러올 수 있게 해주는 태그.<br/>
body태그의 속성정보 이므로 body태그 속성자리에서 사용한다.

- property 
: body.속성명 을통해 속성값을 불러올 수 있다.
- default 
: 해당 값이 없을 때 디폴트값 설정
- writeEntireProperty 
: true, yes, 1 일 시 속성명까지 명시하게 해주어 속성명을 지정할 필요가 없다.
{% highlight ruby %} 
<body
	id="<decorator:getProperty property="body.id" default="a"/>"
	<decorator:getProperty property="body.class" writeEntireProperty="true" />
	<decorator:getProperty property="body.style" writeEntireProperty="true" />
	<decorator:getProperty property="body.onload" writeEntireProperty="true" />
></body>
// 원본태그 <body id="bo" class="bocl" style="background:red;"> 등의 정보를 불러오게 해준다.
{% endhighlight %}




<br/>