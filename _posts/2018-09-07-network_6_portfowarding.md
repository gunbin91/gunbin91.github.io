---
layout: post
title: "6. 포트 포워딩 ( port forwarding )"
tags: [ network, port, 파이썬 ]
date: 2018-09-07
categories: [ network ]
---

<p align="center">
    앞장에서 설명한 외부에서 사설IP로 접근할 수 있도록 하는 기술인 포트포워딩에 대해 알아보자.
</p><br/>

# 포트 포워딩 ( port forwarding )
외부에서 사설IP에 구동중인 서버에 접근을 할 수 있도록, 라우터(공유기)의 포트 중 하나를 해당 사설IP에 연결시켜 <font color="deeppink">외부에서 라우터에 설정한 포트로 접근 시 해당 사설IP로 접근할 수 있도록 하는 기술</font>이다.

<br/>

# 포트 포워딩 설정방법
웹 브라우저의 주소창에 라우터의 사설IP를 입력 후 라우터로 접속하여<br/><font color="orange">'고급설정' -> 'NAT/라우터관리' -> '포트포워드 설정'</font>으로 들어가 아래와 같이 설정한다.<br/>

- 규칙이름 : 아무 이름이나 설정
- <font color="deeppink">내부 IP주소</font> : 서버를 설치한 사설IP의 주소를 설정 ( ex ) 192.168.0.4 )
- <font color="deeppink">외부포트</font> : 외부에서 사설IP의 서버로 접근할 때 라우터의 포트번호를 지정
- <font color="deeppink">내부포트</font> : 서버가 설치된 사설IP의 포트번호

> 외부에서 <font color="orange">'라우터의공용IP:외부포트'</font>로 접근하게 되면, 라우터가 자동으로 <font color="orange">'내부IP주소:내부포트'로 연결</font>시켜주어 외부에서 사설IP의 서버로 접근이 가능해진다.<br/><br/>
ex )
- 내부 IP주소 : 192.168.0.4
- 외부포트 : 8081
- 내부포트 : 80<br/>
=> <font color="orange">'공용IP:8081'</font>로 접속할 시 라우터의 사설IP망의 <font color="orange">'192.168.0.4:80'</font>으로 접속하게 된다. 

<br/>