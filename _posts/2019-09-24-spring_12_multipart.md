---
layout: post
title: "12. 스프링 MultiPart 파일처리"
tags: [ spring, multipart ]
date: 2019-09-24
categories: [ spring ]
---

<p align="center">
    기존 JSP에서도 파일 업로드 처리를 할 수 있었지만, Spring에는 좀 더 쉽게 파일을 업로드할 수 있는 기능을 지원한다.
</p><br/>

## ◆ 스프링의 Multipart파일처리
스프링은 multipart처리를 위한 서포트를 지원한다.<br/>
디폴트로는 지원이 꺼진 상태로 되어있으며, 전자정부프레임워크에서는 디폴트가 켜져 있는 상태다.<br/>

> 물론, <font color="hotpink">스프링에서도</font> HttpServletRequest를 인자로 하는 컨트롤러를 만들어서 <font color="hotpink">MultipartRequest객체로 처리하는 기존의 방식이 가능</font>하지만, Spring에서는 <font color="hotpink">MultipartResolve를 통해 더 간단하게 파일처리를 할 수 있다.</font>

<br/>

### ▶ 라이브러리 추가
CommonsMultipartResolver를 사용하기 위해서는 Apache Commons FileUpload 라이브러리를 메이븐에 추가하여야 한다.
{% highlight ruby %}
<!--https://mvnrepository.com/artifact/commons-fileupload/commons-fileupload-->
<dependency>
    <groupId>commons-fileupload</groupId>
    <artifactId>commons-fileupload</artifactId>
    <version>1.3.3</version>
</dependency>
{% endhighlight %}

<br/>


### ▶ 멀티파트 객체등록
IOC컨테이너에 <font color="orange">id를 반드시 multipartResolver로 하는</font> 아래 두 객체중 하나를 등록한다. <br/>
( 스프링에서 해당 아이디를 인식하기 때문에 id는 반드시 multipartResolver로 해야한다 )

- org.springframework.web.multipart.commons.CommonsMultipartResolver ( 추천 )
- org.springframework.web.multipart.support.StandardServletMultipartResolver

{% highlight ruby %}
<bean id="multipartResolver"
class="org.springframework.web.multipart.commons.CommonsMultipartResolver">
    <property name="uploadTempDir" value="/temp"></property> // 임시디렉터리
</bean>
{% endhighlight %}
- uploadTempDir
: 파일을 실제로 업로드 하기 전에 파일이 임시로 저장되는데, <font color="hotpink">uploadTemDir은 임시로 저장될 파일의 디렉터리를 지정</font>하는 옵션으로, <font color="hotpink">업로드처리를 하지 않거나 업로드처리 이후에는 해당 임시파일은 삭제</font>된다.<br/>
( 여러 개의 파일을 동시에 올렸을 경우에는 임시파일로 하나의 파일에 여러 개가 합쳐지기 때문에 분리해서 처리해야 한다. )

<br/>

### ▶ 컨트롤러에서 받아오기
컨트롤러에서 파일객체를 불러올 때 별다른 처리 없이 메서드의 인자로 <font color="orange">@RequestParam 타입을 MultipartFile</font>객체로 받아오기만 하면된다.<br/>
( 단, 마찬가지로 input name과 일치해야 함 )<br/>
ex)<br/> 
- @RequestParam MultipartFile 인풋네임
- @RequestParam("인풋네임") MultipartFile 변수
- 파일이 multiple일 경우: @RequestParam MultipartFile[] 인풋네임

> multiple은 하나의 인풋파일에 여러개의 파일을 선택할 수 있는 옵션이다. <br/>
&lt;input type="file" multiple>하게되면 같은 인풋네임으로 여러개의 파일이 넘어온다.<br/>
또는 같은 인풋네임의 여러 인풋태그가 넘어올 때도 같은방식으로 넘어온다.

- ※주의: 파일이 없을 때도 객체에 담겨오기 때문에 하나의 파일을 전송할 경우 <font color="orange">isEmpty()로 파일이 넘어왔는지 확인</font> 후 작업을 해야 한다.

<br/>

### ▶ 파일 업로드
받아온 객체를 업로드 처리하지 않으면 임시파일에 저장된 파일이 자동적으로 삭제되기 때문에 <font color="orange">MultipartFile객체의 transferTo(File f) 메서드를 이용해서 업로드처리</font>를 해야 한다.

- 1) 리네임과 동시에 파일객체 생성
: 파일객체는 실제 경로로 지정해야 하기 때문에 <font color="orange">application객체를 뽑아서 realPath로 디렉토리를 설정하고, 두 번째 인자로 파일의 리네임</font>을 정한다.<br/>
단, 해당 디렉터리 경로가 없을 경우 자동적으로 생성하지 않기 때문에 없으면 mkdir()로 디렉터리부터 생성해야 한다.
{% highlight ruby %}
File file = 
new File(request.getServletContext().getRealPath("/temp"), “random”);
{% endhighlight %}

- 2) transferTo() 업로드
: 위에서 만든 파일객체의 경로와 리네임으로 실제 업로드 하기위해transferTo()메서드로 업로드처리를 한다. <font color="orange">MultipartFile객체.transferTo(file)</font>
{% highlight ruby %}
// @RequestParam MultipartFile f 일 때
File file = new File(request.getServletContext().getRealPath("/temp"), "test.png");
f.transferTo(file);
{% endhighlight %}

- 실제 파일 경로
: <font color="orange">apache-tomcat-8.5.45(서버)\webapps\프로젝트디렉터리를 루트</font>기준으로 저장된다.<br/>
ex) "\temp"로 저장한다면? apache-tomcat-8.5.45(서버)\webapps\프로젝트디렉터리\temp
<br/>파일을 html등에서 다시 <font color="orange">불러올 시에는 getRealPath없이</font> 불러오면 된다.

<br/>

### ※ 주의사항

- 이클립스에서 실행하는 서버와 실제 서버는 다르다
: 이클립스에서 실행하는 서버는 테스트 서버이기 때문에 실제 파일이 저장될 경로도 달라지게 된다.<br/> <font color="orange">실제 파일을 서버에 저장시키기 위해서는 프로젝트를 war파일로 만들어 서버의 webapp디렉터리에 넣어야 한다.</font> <a href="/jsp/2019/05/13/jsp_2_setting.html">WAR파일 만들기 참고</a>

<br/>

- enctype주의 
: 기존 MultipartRequest처리 방식처럼 <font color="orange">모든 파일처리는 post방식에 enctype이 multipart/form-data</font>이어야 한다. <a href="/jsp/2019/05/28/jsp_11_file.html">MultipartRequest처리</a>참고

<br/>

- 일부 tomcat버전 context.xml파일 수정 필요
: 일부 톰캣 버전에서는 별도의 설정이 필요하다. <font color="hotpink">에러가 발생할 경우 (톰캣)apache-tomcat-8.5.45\conf\context.xml파일을 수정</font>해야한다.
<br/>&lt;Context>태그와 &lt;Resources>태그의 옵션을 추가해준다.
{% highlight ruby %}
<Context allowCasualMultipartParsing="true" path="/">

	<!-- Default set of monitored resources. If one of these changes, the -->
	<!-- web application will be reloaded. -->
	<WatchedResource>WEB-INF/web.xml</WatchedResource>
	<WatchedResource>${catalina.base}/conf/web.xml</WatchedResource>

	<!-- Uncomment this to disable session persistence across Tomcat restarts -->
	<!-- <Manager pathname="" /> -->
    <Resources cachingAllowed="true" cacheMaxSize="100000" />
</Context>
{% endhighlight %}





<br/>