---
layout: post
title: "3. NAT( NetworkAddressTranslation )"
tags: [ network, NAT, 파이썬 ]
date: 2018-09-07
categories: [ network ]
---

<p align="center">
    Network Address Translation의 약자인 NAT에 대해 알아보자.
</p><br/>

# NAT ( Network Address Translation ) 
공유기환경의 컴퓨터가 즉, <font color="deeppink">사설IP를 쓰고 있는 컴퓨터가 다른 사이트(서버)로 접속 하려고 할 때</font><br/>같은 공용IP를 공유하고 있는 LAN에 있는 서버가 아닐 시, WAN을 통해 접속을 해야 하는데,<br/>사설IP는 외부 다른 서버에 접근이 불가하다. 따라서 이때 <font color="deeppink">NAT(네트워크주소변경)</font>이라는 것을 사용한다.

# NAT 동작 구조
사설IP로 외부 다른 서버에 접속(요청)을 할 수 없기 때문에 해당 <font color="orange">사설IP를 라우터가 가지고 있는 공용IP로 변환 후 요청</font>을 해야한다.<br/>

<img src="{{ site.baseurl }}/assets/post_img/nat.jpg" align="left"><br/>
<br/>
[출처] <a href="https://www.youtube.com/watch?v=kw6xNjqKm-E" style="text-align:center;">https://www.youtube.com/watch?v=kw6xNjqKm-E</a><br/>

- 사설IP가 외부 서버에 응답요청시 라우터는 사설IP의 기록을 남겨두고,<br/>NAT를 이용해 공용IP로 주소를 바꾼 후 서버로 요청한다.<br/><br/>
- 서버로 부터 응답이 올 시 공용IP를 통해 라우터로 응답들어오면,<br/> 공용IP를 라우터에 기록으로 남겨둔 사설IP로 다시 NAT를 이용해 사설IP로 바꾼 후 응답을 받는다.
<br/><br/>


<br/>