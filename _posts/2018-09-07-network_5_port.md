---
layout: post
title: "5. 포트 ( Port )"
tags: [ network, port ]
date: 2018-09-07
categories: [ network ]
---

<p align="center">
    네트워크 상의 통신을 할 때 필요한것은 IP주소 뿐만이 아니다.<br/> 하나의 IP주소에 여러 Port라는 것이 존재하는데 이에대해 알아보자.
</p><br/>

# PORT ( 포트 )
컴퓨터에는 65535개의 포트가 있으며, 그중에 22번 Port는 SSH, 80번 Port는 http이다.<br/> 
즉, 기본적으로 <font color="deeppink">http프로토콜을 이용하는 웹은 포트번호가 80</font>이다.<br/><br/>
또한 0~1023번의 포트번호는 이미 예약되어 있는 포트번호(Well-known port)로서 임의로 사용할 수 없다.<br/>
( 참고로 관습적으로 80번 포트에 서버를 설치하지 못하는 경우 8080에 설치 하고있다. )

<br/>

# URL ( 인터넷주소 )
URL의 기본 구조는 <font color="orange">'통신규약://도메인네임:포트번호'</font>이고, 브라우저의 디폴트 포트번호는 80으로 설정되어 있기 때문에 접속하고자 하는 <font color="deeppink">서버의 포트번호가 80일 경우에는 생략이 가능</font>하다.<br/><br/>

- 즉, 80번 포트에 설치되어 있는 서버에 접속 할 경우 주소(IP)만 입력하면 되고, 80포트가 아닌(ex)8080)포트에 접속할 경우 주소 뒤 포트번호(ex ) http://foods.saansoo.org:8080)를 적어주어야 한다.<br/>

# 사설 IP로 서버 구동 시 외부에서 접속이 불가한 이유?
외부에서 사설IP에 설치된 서버에 접속하고자 할 때, 라우터의 공용IP를 통하여 접근 하게 되는데,<br/>
라우터는 어떤 사설IP로의 접속을 하는 것인지 알지 못하기 때문에 응답을 줄 수가 없다.<br/><br/>
따라서, <font color="deeppink">사설IP의 서버에 외부접근이 가능하도록 하기 위해서는 라우터의 포트중 하나를 서버를 구동 하고자하는 사설IP로 연결 시켜주도록 설정</font>하면 된다. 이를 <font color="deeppink">'포트포워딩(PortForwarding)'</font>이라고 한다.

<br/>