---
layout: post
title: "8. DHCP"
tags: [ network, dhcp, 사설ip 수동설정  ]
date: 2018-09-07
categories: [ network ]
---

<p align="center">
    공용IP를 공유하는 기기들의 사설IP를 할당해주는 DHCP에 대해 알아보자.
</p><br/>

## DHCP( Dynamic Host Configuration Protocol )
라우터에 통신기기들을 연결하게 되면, <font color="deeppink">사설IP가 자동으로 부여</font>되는데 원래는 수동으로 해야 할 일을 DHCP라는 규약을 이용해 해주는 것이다.

#### ▶ DHCP 동작원리
기본적으로 <font color="orange">라우터에는 DHCP Server</font>가 내장되어 있고, <font color="orange">통신 기기에는 DHCP Client</font>가 내장 되어있다.<br/>
( 물론 라우터 또한 통신 기기이다. )<br/>
또한 모든 통신기기들에는 물리적인 주소인 MAC주소를 가지고 있는데, 통신기기에서 라우터를 통해 인터넷에 연결하게 될 때 라우터에 있는 <font color="orange">DHCP Server에 통신기기의 Mac주소와 비어있는 사설IP주소를 매치해 저장</font>해 놓게 되며, 마찬가지로 또 다른 통신기기에서 라우터와 연결 시 자동으로 해당기기의 Mac주소에 비어있는 사설IP를 할당해 주게 된다.

#### ▶ DHCP 설정변경
<font color="orange">기본게이트웨이(라우터의 사설IP)로 접속 -> 관리 -> 고급설정 -> 네트워크 관리 -> 내부 네트워크 정보</font>로 들어가 해당 라우터를 사용중인 통신기기의 현재 할당 사설IP주소와 MAC주소와 연결 방식을 확인할 수 있다.<br/><br/>
"내부 네트워크 설정"에 들어가 보면, DHCP를 설정할 수 있는데 "IP대여시간"이라는 것을 통해 <font color="orange">사설IP또한 유동IP</font>라는것을 확인할 수 있고,
'동적 IP주소 범위'를 통해 자동으로 할당되는 사설IP주소의 범위를 설정할 수도 있다.

# 수동으로 사설 IP설정하기
사설IP부여를 DHCP가 아닌 수동으로 하기 위해 <font color="orange">제어판 -> 네트워크 및 인터넷 -> 네트워크 및 공유센터 -> 연결:이더넷 클릭 -> 속성 -> 인터넷 프로토콜 버전 4 (TCP/IPv4) 선택 -> 속성</font>에서 아래와 같이 설정할 수 있다.<br/>

<img src="{{ site.baseurl }}/assets/post_img/ipv4.jpg" height="250px" style="padding:0;margin:0;">

- '다음 IP주소 사용' 선택
- IP주소 : 수동 사설IP설정
- 서브넷마스크 : ?
- 기본 게이트웨이 : 공용IP
- 기본 DNS 서버 : ?
- 보조 DNS 서버 : ?

이처럼 수동으로 IP를 설정하기 위해서는 기본적인 지식이 있어야 하고 번거롭기 때문에 
DHCP를 이용하여 자동적으로 설정하게 된다.

<br/>