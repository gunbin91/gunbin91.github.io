---
layout: post
title: "2. 웹 프로그래밍 개요 및 설정"
tags: [ jsp ]
date: 2019-05-13
categories: [ jsp ]
---

<p align="center">
    웹 프로그래밍의 전반적인 개요와 JSP설정법에 대해 알아보자.
</p><br/>

# ◆ 웹 어플리케이션 ( 프로그램 )
인터넷 혹은 인트라넷을 통해 브라우저를 이용하여 사용되어지는 프로그램 <br/>
( 예매, 업무공유, 쇼핑, 게임, 정보 공유, 은행업무, 수강신청 등등 )

<br/>

# ◆ 웹 프로그램이 인기를 끌게 된 배경 
- 사용자 측 
: 별도의 설치 프로그램 없이도, 서비스를 제공받을 수 있다. 접근이 용이
- 개발자 측 
: 사용자 UI 프로그램을 만들지 않아도 된다.<br/>
브라우저에 의해서 해석되는 문서(HTML)를 제공해주면 되기 때문에

<br/>

# ◆ 웹 프로그램 언어
- java(Servlet/JSP), C(ASP), php(PHP), python(Django/Flask)등등 여러 프로그래밍 언어가 있다.
- java를 이용한 웹 프로그램
: 서블릿(Servlet) 또는 JSP둘 중 하나만 알아도 개발은 가능하다.<br/>
(jsp가 서블릿으로 변환되기 때문)

<br/>

# ◆ 개발환경 구축
<b>1. JDK ( 설치 ) - 자바와 동일하게 셋팅하면 된다.</b>
<b>2. 웹 개발용 IDE설치(통합 개발 환경 - TOOL) -> 이클립스 EE 설치</b><br/>
=> 새로 받거나, 기존 사용 중이던 버전에 웹 개발 플러그인을 설치<br/>

이클립스 -> help -> eclipsemarket -> allMarket을 eclipse project로 변경 -> java EE ( web develope ) 설치
<br/>
- 설치확인
: create new project >> web관련이 있는지 확인 또는 help -> about eclipse에서 확인

> 단순한 자바 프로그램은 J2SE를 사용하지만, 웹 환경의 자바를 구동하려면 J2EE를 사용해야 한다.

<b>3. WAS ( Web Application Server) 설치</b>

- https://tomcat.apache.org 접속하여 사용하고자 하는 tomcat버전을 zip파일로 설치
- Eclipse에서 Server탭클릭(없을 경우 window->show view->server선택) 새로운 서버를 추가하여 다운받은 버전에 맞는 tomcat버전 선택 후 다운받은 tomcat 디렉터리로 설정

<br/>

## ▶ WAS
java로 만들어진 웹 프로그램을 가동시켜주는 서버(꼭 자바는 아님)로
종류도 다양함<br/>
tomcat(★) resin, jboss, jonas, weblogic ....등등<br/>

- 설치확인
: 19년5월기준 tomcat.apache.org - 버전 8.5 대를 사용하겠다.<br/>
톰캣zip 압축을 풀고 bin -> startup.bat 을 실행
> C:\Program Files\Java\jre1.8.0_144 ( JRE_HOME ) 이나<br/>
C:\Program Files\Java\jdk1.8.0_144 (JAVA_HOME) 등이 환경변수로 잡혀있어야 함

<br/>

#### ▶ 웹 프로그램 실행
프로그램은 톰캣 폴더에 <font color="orange">webapps라는 폴더에 실제 만들어진 프로젝트를 넣어서 실행</font> 하는 것이다.<br/>
서버를 켜둔 상태에서 자신의 IP:8080/webapp안에폴더경로.html를 치게 되면 프로그램이 정상 가동되는지 확인할 수 있다. <br/>( 자기 ip는 127.0.0.1 로 치면 알아서 잡아냄 )

- 서버경로
: <font color="orange">ip: 포트번호 / webapp안 프로젝트경로</font>
웹 브라우저에서 서버에 접근하는 방법은 위와 같으며, [ip:포트번호]까지가 webapp 까지의 경로이다.<br/>

> 웹브라우저는 http 요청을 보낼 때 포트 지정을 하지 않는다면 디폴트로 상대방의 80번 포트로 요청을 보낸다.<br/>
=> 따라서 톰캣자체의 포트번호를 80번호로 수정하게 되면 일일이 포트번호를 치지 않고서도 80번으로 자동 접속 되게 된다. )

<br/>

#### ▶ 톰캣 서버 설정
이클립스에서 추가된 서버를 더블클릭하면 서버 설정창이 나온다
- Server Locastions항목을 “Use Tomcat installation”으로 선택
- Server Options항목에 Publish module contexts to separate XML files를선택
- Ports항목의 http포트를 8080이 아닌것으로 수정 ( 오라클에서8080을 사용하기 때문에)

위의 방법은 해당 프로젝트에서만 적용되는 사항이고, 실제 톰캣의 디폴트 포트설정은 xml파일을 열어 설정해준다.<br/>

( 톰캣폴더 /conf/server.xml 를 수정 )  -> Connector port = 8080을 80으로 수정
하면 포트번호를 일일이 지정해주지 않아도 된다.<br/>
( 브라우저의 디폴트값이 80이기 때문에 맞춰주는 것 )

+ @ 최신 HTML5를 지원하는 표준 브라우저 / chrome, firefox을 설치 ( 익스플로러 X　)

<br/>

# ◆ 웹 프로그램 개발
java 기반의 웹 프로그램 개발 방법에는 두 가지의 방법이 있다. <br/>
하나는 servlet을 이용한 방법이 있고, 두 번째로는 jsp를 서블릿으로 변환하는 방법이다.

<br/>

#### ▶ 서블릿을 이용하여 웹 프로그램 개발
- Servlet 
: 클라이언트 측의 웹 요청에 의해 작동되게 설계되어진 클래스.<br/>

- 웹 프로젝트 생성방법
: 이클립스에서 dynamic web project를 생성 next->next-> <font color="orange">Generate web.xml deployment descriptor 체크</font>하고 생성<br/>
(해당 옵션을 체크해야 web.xml을 자동적으로 생성해준다.)

- 서버실행
: 1. 프로그램 코드 작성 후 프로젝트 우 클릭 -> export -> war file 생성<br/>
2. war파일을 톰캣의 webapps폴더로 복사. ( 업로드 )
3. startup 실행 시 webapps에 프로젝트 파일이 생김
4. ip/ 프로젝트/ url-pattern에 등록한 패턴(web.xml) 을 주소창에 입력하면 접속!

>정석적인 방법은 위의 방법이 맞지만, 학습단계에서 was를 직접 제어해서 프로그램 테스트하기가 번거롭기 때문에 이클립스를 통해서 제어가 가능하다.

- Eclipse 테스트 서버실행
: new -> server -> apache tomcat 8.5 -> 톰캣 설치 경로로 잡고 만들기<br/>
=> servers가 생기고, tomcat서버를 실행시킬 필요가 없어짐. ( 테스트 서버가 만들어짐 )<br/>
=> 밑에 Servers탭에서 톰캣8.5 우클릭 -> add and remove에서 프로젝트 add<br/>
=> 서버를 이클립스에서 실행시켜서 똑같은 방식으로 접속하면 됨.

<br/>

# ◆ JSP 주소 패스 바꾸기
서버 실행후 접근 시 서버의 ip:포트 다음 프로젝트명을 적어주어야 하지만, 이를 프로젝트명 없이 접근이 가능하도록 설정할 수 있다.
<br/>
server(더블클릭) -> Module탭 ->해당 프로젝트 edit -> path 변경<br/>
해당 path를 /로 바꿔주면 프로젝트명을 일일히 적어서 접근할 필요가 없다.

>단, 서버에 add and remove 로 프로젝트를 add 시켜놓아야 수정이 가능하다.<br/>
=> 또한 새로운 프로젝트를 생성할 때마다 라이브러리를 추가 시켜줘야 한다.
( jsp-api.jar , servlet-api.jar )










<br/>