---
layout: post
title: "4. IP Address 알아내기"
tags: [ network, IpAddress, public ip, private ip, 파이썬 ]
date: 2018-09-07
categories: [ network ]
---

<p align="center">
    사설IP와 공용IP의 주소를 알아내는 방법에대해 살펴보자.
</p><br/>

# Private IP Address(사설IP) 찾기 

#### ▶ Window 

<font color="deeppink">제어판 -> 네트워크 및 공유센터 
    -> 연결:이더넷 or 연결:와이파이 클릭 -> 자세히</font><br/>

<img src="{{ site.baseurl }}/assets/post_img/window_ip.JPG" height="250px" style="padding:0;margin:0;">

- <font color="orange">IPv4주소</font> : 현재 기기의 사설 IP주소
- <font color="orange">IPv4 기본 게이트웨이</font> : 라우터(공유기)의 사설 IP주소
<br/><br/>

또는 <font color="deeppink">CMD(명령프롬프트) -> 'ipconfig'입력</font>
<br/>

<img src="{{ site.baseurl }}/assets/post_img/cmd_ip.JPG" height="250px" style="padding:0;margin:0;">

- <font color="orange">IPv4주소</font> : 현재 기기의 사설 IP주소
- <font color="orange">기본 게이트웨이</font> : 라우터(공유기)의 사설 IP주소

#### ▶ Linux
<font color="deeppink">터미널 -> 'ifconfig'입력</font>
- <font color="orange">inet addr</font> : 사설 IP주소
<br/>

<font color="deeppink">터미널 -> 'route'입력</font>
- <font color="orange">default Gateway</font> : 라우터 사설IP

# Public IP Address(공용IP) 찾기
공용IP 주소를 알아내는 방법에는 크게 두 가지가 있다.<br/>

- 웹 브라우저 주소창에 <font color="orange">IPv4기본 게이트웨이(라우터의 사설IP)를 입력하여 접속 -> 관리자모드</font>의 <br/><font color="deeppink">외부IP 주소가 공유기의 공용IP</font>이다.<br/>
( 단, 이 방법은 이중 라우터로 되어 있을 시 확실 치 않음. 또한 라우터 관리자 권한이 있어야 함. )<br/><br/>

- 아무 <font color="orange">검색엔진에 접속하여 'ip주소 확인'을 검색</font>하면 해당 기기의 공용IP주소를 알려준다.<br/>
또한 해당 주소가 정확한 공용IP의 주소이다. 왜냐하면 <font color="deeppink">서버와 클라이언트간의 통신은 공용IP를 통해서만 가능</font>하기 때문이다.


<br/>