---
layout: post
title: "2. 공유기(라우터)의 작동원리"
tags: [ network, router ]
date: 2018-09-06
categories: [ network ]
---

<p align="center">
    공유기와 라우터는 같은 의미이다. <br/>하나의 인터넷을 여러 기기에서 나눠 쓸 수 있게 해주는 공유기의 작동원리를 알아보자.
</p><br/>

# 기본 통신 방법
클라이언트가 서버의 IP로 접속하게 될 때 동시에 클라이언트의 IP또한 서버로 전달된다.<br/>
즉, 서버와 클라이언트 서로간 IP정보를 계속해서 주고 받기 때문에 <font color="deeppink">서버/클라이언트가 통신하기 위해서는 서로간의 IP address를 알아야 한다.</font>

# IP address 부여
통신사와 계약하여 케이블 회선을 받아 인터넷에 접속할 수 있는 기기(스마트폰 or PC)가 <font color="deeppink">인터넷에 접속(와이파이 or 유선)하게되면 그 순간 해당 기기에 IP가 부여</font>된다.<br/>
따라서 인터넷을 사용하고 있는 모든 기기에는 IP주소라는 것이 존재한다.

# 공유기 사용이유 ? 
일반적으로 인터넷 통신사와 계약을 하면 하나의 케이블을 받을 수 있게 되고,<br/>
해당 <font color="deeppink">케이블을 통해 하나의 IP가 부여</font> 되기 때문에 동시에 여러개의 인터넷을 사용할 수가 없다.<br/>

- 따라서 여러개의 인터넷 기기를 사용하고자 할 경우 케이블을 여러개 받게 되면 되지만, 경제적인 부담이 늘어나기 때문에 하나의 IP주소를 공유할 수 있는 공유기를 쓰는것이다.

# 공유기(라우터) 작동원리
공유기에는 두 종류의 잭단자인 WAN과 LAN이 있다. 

- <font color="orange">(WAN)WideAreaNetwork</font><br/>
통신사로부터 부여받은 케이블을 꽂는 단자로, <font color="deeppink">케이블을 WAN단자에 연결하게 되면 통신사로부터 부여받은 IP는 공유기가 차지</font>하게 된다.<br/>
또한 이렇게 부여받은 IP는 전세계 어디서든 바로 접근할 수 있는 IP로 <font color="orange">public IP address(공용IP)</font>라고 부른다.<br/>
ex ) 59.6.66.238
<br/><br/>

- <font color="orange">(LAN)LocalAreaNetwork</font><br/>
하나의 인터넷 케이블을 공유할 기기들을 유선으로 연결할수 있는 단자로 유선이든 무선이든 근본은 같다.
( 회사의 내선 전화(회사 내에서 쓰이는 번호)와 비슷한 개념 )<br/>
이렇게 LAN을 통해 연결된 기기들 또한 IP주소는 부여받는다. 또한 공유기도 해당 IP를 받게된다. 
즉, 공유기는 IP가 두개(공용IP/사설IP)인 것이다.<br/>
하지만 이때 받게 되는 IP주소는 <font color="orange">private IP address(사설IP)</font>라고 하며, <font color="deeppink">사설 IP의 경우 외부에서 바로 접속할 수 없다.</font>
ex ) 192.168.0.1  

# 공용IP / 사설IP

#### ▶ <font color="orange">public IP address(공용IP)</font> 
즉, 통신사와 계약을 통해 들어온 케이블은 public IP address(공용IP)이고 <font color="deeppink">공용IP는 외부에서 바로 접근이 가능</font>한 IP주소이다.

#### ▶ <font color="orange">private IP address(사설IP)</font>
통신사로 부터 직접적으로 부여받은 IP가 아닌 공유기를 통해 나눠진 기기들의 IP는 private IP address(사설IP)이고 <font color="deeppink">사설IP는 외부에서 바로 접근이 불가</font>하고, 기본적으로 같은 공용IP를 공유하는 기기들 끼리만 접근이 가능하다.

> 192.168.~.~ 대의 주소는 사설 IP (약 6만개)이고,<br/>
그 이하의 주소는 공용IP가 된다.<br/>
즉, 공용IP는 중복될 수 없지만, 사설IP는 중복될 수 있다.


<br/>