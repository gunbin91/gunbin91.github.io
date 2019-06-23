---
layout: post
title: "3. window객체"
tags: [ javascript window ]
date: 2019-05-25
categories: [ javascript ]
---

<p align="center">
    자바에서 object처럼 자바스크립트에서도 최상위 객체처럼 쓰이는 window객체라는 것이 있다.<br/>
    window객체는 브라우저를 제어할 수 있는 가장 기본적인 객체이다.
</p><br/>

# ◆ window객체
window 객체는 브라우저 내에 떠있는 창을 대표하는 객체

<br/>

#### ▶ 윈도우 객체 속성
- window.outerHeight
: 브라우저 전체 높이 크기
- window.outerWidth
: 브라우저 전체 넓이 크기
- window.innerHeight
: 브라우저 내의 페이지 높이 크기
- window.innerWidth
: 브라우저 내의 페이지 넓이 크기
- window.screenX
: 왼쪽제일위를 기준으로 스크린의 x좌표
- window.screenY
: 왼쪽제일위를 기준으로 스크린의 y좌표
- window.screenLeft
: 왼쪽제일위를 기준으로 스크린의 x좌표
- window.screenTop
: 왼쪽제일위를 기준으로 스크린의 y좌표
- window.document
: 이 윈도우가 가지고 있는 html문서 부분 정보를 담고 있는 객체
- window.history
: 윈도우 이동 기록 정보를 담고 있는 객체
- window.location
: 윈도우의 위치 정보를 담고 있는 객체
- window.console
: 이 윈도우에 딸려 있는 console 정보를 담고 있는 객체

> window객체는 스크립트에서 this개념과 비슷하다. 따라서 <font color="orange">window객체 소속으로 있는 속성이나 함수들은 window키워드를 생략해서 사용</font>할 수 있다.

<br/>

#### ▶ window객체 함수
- alert(), prompt(), confirm()
: dialog 띄우기
- setInterval(), clearInterval()
: 특정함수의 반복처리

<br/>

# ◆ window객체를 이용한 팝업창 제어

<br/>

#### ▶ 팝업창 열기

- var d = window.oepn()
: 새 브라우저(팝업창)를 띄울 수 있다.
{% highlight ruby %}
open("sub.jsp"); 
open("http://www.naver.com");
{% endhighlight %}

<br/>

#### ▶ 팝업창 닫기
- window.close();
: close()는 open()으로 만들어진 브라우저만 가능하고, <font color="orange">해당 브라우저를 닫기 위해서는 open()시에 반환된 객체</font>를 가지고 있어야 한다.<br/>
( open()시 반환되어 만들어지는 객체는 새로운 window객체이다. 또는 새로 열린 팝업창 내에서의 window객체로 닫을 수 있다.)
{% highlight ruby %}
var d = open("~.jsp");  
d.close();
{% endhighlight %}

<br/>

#### ▶ open() 매개인자 설정
팝업창을 open()메서드를 통해서 열 경우, 몇 가지의 인자를 붙일 수 있다.
1. 팝업창을 열 페이지의 경로(string)
2. 팝업창의 이름 (string)
3. 팝업창의 크기 및 위치 (string)

- 팝업창의 이름을 설정하지 않으면, 중복으로 여러 개를 계속해서 띄울 수가 있다.
- 팝업창의 이름을 설정하게 될 경우, 동일한 이름의 팝업창은 하나의 팝업창이 전환되는 형식.
- 팝업창의 크기 및 위치 설정은 "left=100,width=400,top=200,height=100" 의 형식으로 하게 되고, 비어있는 두 번째 인자에 공백 스트링(“”)을 넣게 되면 없는 이름으로 처리가 된다. 
{% highlight ruby %}
open("http://www.naver.com", "","left=100,width=400,top=200,height=100");
{% endhighlight %}

<br/>

#### ▶ 팝업창에서 부모페이지의 윈도우 제어
팝업창에서 해당 팝업창을 불러온 페이지의 window객체를 제어하고자 할 경우 <font color="orange">window.opener</font>로 부모 페이지의 window객체를 반환받을 수 있다.<br/>
따라서 팝업창에서 부모페이지를 제어하려면 해당 객체가 필요하다.<br/>
( 즉, 팝업창이 아닌 경우 의미가 없게 되며, <font color="orange">팝업창에서 자신을 끄려면 window.close()</font> 하면된다. )<br/>
- window.name : 현재 윈도우의 이름

<br/>

# ◆ window.history 객체
브라우저의 윈도우 이동 기록 정보를 담고 있는 객체

<br/>

#### ▶ history 속성
- history.length 
: 보관하고 있는 history개수

<br/>

#### ▶ history 함수
- back()
: 이전페이지로 이동하는 함수 ( 뒤로가기 버튼과동일 )
- forward()
: 앞 페이지로 이동하는 함수
- go(n)
: n만큼 페이지 이동 ( back()는 go(-1)과 동일, forward()는 go(1)과 동일 )
<br/>

- 자바의 response.sendRedirect() 메서드는 새로운 요청을 발생시키지만, history객체는 그냥 이전 페이지들의 마지막 상태를 보여주는 기능이다.

<br/>

# ◆ window.location
문서 정보를 담당하고 있는 객체

<br/>

#### ▶ location 속성
- location.href 
: 전체 URL 반환
- location.origin 
: protocol, hostname, port 반환 ( ip )
- location.pathname 
: ip를 제외한 현제 페이지 경로 반환
- location.search 
: 쿼리 스트링 반환

<br/>

#### ▶ 속성을 이용한 페이지이동
위 속성들은 반환해주는 역할도 하지만, 속성을 바꿔서 페이지 전환또한 가능하다.
{% highlight ruby %}
location.href = "http://www.naver.com"; 
{% endhighlight %}
location객체의 href속성을 페이지 경로명으로 수정하게 되면 해당 페이지를 이동 시킬 수 있다.
<br/>주의 ) 절대경로( / 로 시작하는)를 적게 될 경우 ip뒤로 붙게 된다. 또한 pathname을 통해서 페이지전환을 할 경우 무조건 ip뒤로 붙게 되기 때문에 페이지이동은 href를 쓰는것이 좋다.

<br/>

#### ▶ location 함수
- location.reload();
: 현재 경로로 재요청을 보내 문서 갱신. ( 새로고침과 같은 기능 )
- location.assign("/chap07/window/02.jsp");
: 현재페이지의 경로를 바꿈 ( href는 속성 자체를 변환 시키는 것이고, assign은 함수, 기능은 같다. )
- location.replace("/chap07/window/02.jsp");
: 현재 페이지의 경로를 바꾸는 기능은 똑같지만 history의 문서 자체를 바꾸기 때문에 해당 기록이 사라져서 뒤로 가기 등이 먹히지 않게 된다. ( 따라서 자주 쓰이지 않음 )

<br/>

# ◆ window.document
브라우저 HTML문서가 로딩이 되고 난 후 완성이 되는 문서 관리용 객체.

<br/>

#### ▶ document 속성
- document.title 
: 타이틀을 string형태로 반환 ( 변환가능 )
- document.head
: 헤드부분을 오브젝트형태로 반환
- document.body
: 바디부분을 오브젝트형태로 반환

<br/>

#### ▶ document 함수
- document.getelementById("id");
: 해당 아이디로 설정된 태그 객체를 반환<br/>
=> <font color="orange">id는 같은 값으로 하나만 설정할 수 있다.</font> 만약 여러 개를 설정했을 경우 가장 위에 써놓은 id태그 객체가 뽑힘<br/>
=> 해당 태그 안에 여러 태그가 또 있다면, 그 안에 있는 태그들도 해당 id로 포함되는 객체 값들이다.
{% highlight ruby %}
<h2 id="sub">
    어쩌구
    <span class="c2"> 저쩌구 </span> 
</h2>
<script> 
    // 타고들어가는 접근이 가능하다.
    document.getElementById("sub").getElementsByClassName("c2") 
</scirpt>
{% endhighlight %}

<br/>

- document.getElementsByClassName("c1");
: 해당 클래스로 설정된 태그객체들을 배열로 반환<br/>
=> <font color="orange">class는 같은 값으로 여러 태그에 설정이 가능하고, 한 태그는 여러 클래스를 설정</font>할 수 도 있다.<br/>
=> 여러 개의 클래스를 지정할 때는 공백을 구분자로 처리 <br/>
<b>ex ) &lt;div class="c1 c2"></b>
- document.getElementsByTagName("hr");
: 해당 태그객체들을 배열로 반환
- document.getElementsByName("gender");
: 해당 name옵션인 라디오나 체크박스 태그 등 여러 값을 가지고 있는 태그들의 객체를 배열로 반환

<br/>

> 즉, class는 같은 값으로 여러 개의 태그에 설정이 가능하고, id는 태그당 하나밖에 설정할 수 없다.<br/>
또한, 하나의 id를 가지고 있는 태그 안에 여러 class를 가진 태그들을 설정하고 id와 class를 통해 찾아낼 수 있다.







<br/>