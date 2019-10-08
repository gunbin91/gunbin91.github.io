---
layout: post
title: "5. AJAX(비동기 통신)"
tags: [ javascript, ajax, gson ]
date: 2019-05-25
categories: [ javascript ]
---

<p align="center">
    AJAX(Asynchronouse JavaScript And XML)의 약자로 XML과 Javascript를 이용한 비동기 통신이다. <br/>유용하게 쓸일이 많은 기술이므로 잘 알아두자!
</p><br/>

# ◆ AJAX(Asynchronous Javascript And XML) 에이잭스
&nbsp;<font color="hotpink">Javascript와 XML을 이용한 비동기 통신</font>기술이다.<br/>
브라우저 내에 장착되어 있는 요청 객체를 직접 제어해서, 페이지 전환과정 없이 서버 측과 요청을 주고받는 기술이다. 따라서 사용자 입장에서도 빠르게 처리되는것 처럼 보인다.

<br/>

### ▶ 기본사용법
#### 1. 객체생성
AJAX를 사용하기 위해서는 <font color="orange">XMLTttpRequest</font>객체가 필요하다.
{% highlight ruby %}
var req = new XMLHttpRequest();
{% endhighlight %}

<br/>

#### 2. 요청 페이지설정
생성된 객체를 open메서드를 이용해 통신할 페이지를 설정한다. <font color="orange">XMLHttpRequest()객체.open()</font> 
- 인자 1 : method방식 ( get, post)
- 인자 2 : 요청을 보낼 페이지
- 인자 3 : 비동기 여부( 동기: true, 비동기: false )
{% highlight ruby %}
req.open("get", "01Ajax.jsp?data=10", true);
{% endhighlight %}

<br/>

#### 3. 요청
oepn()메서드의 설정내용대로 해당 페이지로 통신을 요청한다.
{% highlight ruby %}req.send();{% endhighlight %}

<br/>

# ◆ AJAX 통신 응답 데이터처리
<br/>

#### ▶ 응답 데이터 가져오기
send()메서드 호출 후 <font color="orange">responseText속성</font>을 통해 해당 페이지의 내용을 불러올 수 있다.
{% highlight ruby %}
XMLHttpRequest객체.responseText
{% endhighlight %}

<br/>

#### ▶ 동기 통신
동기 통신이란 응답페이지와 동기화하여 응답상태가 확인된 후에 데이터를 받아오는 방식이다.<br/>
oepn()메서드의 <font color="orange">세번째 인자인 비동기여부를 false로 하게되면 동기통신</font>으로 설정된다.<br/>

동기통신은 응답이 확인된 후에 데이터를 받아옴으로 <font color="orange">특별한 처리 없이 responseText를 통해 응답 데이터를 확인</font>할 수 있다. 하지만, 비동기 통신에서는 특별한 처리가 필요하다.<br/>
( 동기통신은 권장사항이 아니다. )
{% highlight ruby %}
//동기통신예제
var req = new XMLHttpRequest();
req.open("get", "sub.jsp", false);
req.send();
console.log(req.responseText);
{% endhighlight %}

<br/>

#### ▶ 통신의 상태
{% highlight ruby %}
if(XMLHttpRequest객체.readyState == 0)
    // oepn() 전
if(XMLHttpRequest객체.readyState == 1)
    // oepn() 후
if(XMLHttpRequest객체.readyState == 4)
    // 응답을 받은상태
{% endhighlight %}

위 예제 처럼 동기든 비동기든 <font color="orange">readyState가 4가된 후에 responseText를 통해 데이터를 받을 수 있다</font><br/>
따라서 <font color="orange">동기 상태에서는 send()후에 동기화하여 바로 4의 상태</font>가 되지만,<br/>
&nbsp;<font color="orange">비동기 상태에서는 send()한 후 바로4상태가 되는 것이 아니다. 따라서 비동기 통신의 경우 별개의 처리가 필요하다.</font><br/> 

> 비동기 통신에서는 하나의 함수가 호출되는 동안 readyState가 4가 되는 것이 불가능, send() 후 다른 함수를 통하여 4의 상태 값을 확인하는 것은 가능하다.

<Br/>

#### ▶ 비동기 통신의 데이터 응답
비동기 상태에서는 readyState==4를 바로 받아올 수 없기 때문에 readyState가 변화할 때마다 자동 호출되는 이벤트 함수인 readystatechange함수를 오버라이드 해야 한다.<br/>

- 함수정의
{% highlight ruby %}
req.onreadystatechange = function() {
    if (this.readyState == 4) { // readState가 4가되었을 때
        window.alert(this.responseText);
    }
}
req.send();
// 위에서 on메서드로 등록을 해놓았기 때문에 send()는 어디에 해도 상관없음
{% endhighlight %}
비동기 통신의 이러한 방법은 동기통신에서도 가능하다.

{% highlight ruby %}
// 비동기 통신 예제
var req = new XMLHttpRequest();
req.open("get", "sub.jsp", true);
req.send();
req.onreadystatechange = function() {
	if (this.readyState == 4) {
		console.log(this.responseText);
        }
}
{% endhighlight %}

<br/>

# ◆ XML
위에서 다뤘듯이 Ajax는 XML과 통신하기 위한 방법이다. 통신 데이터가 복잡해 질 경우 이를 처리하기 힘들기 때문에 태그단위로 만들어지는 XML과 통신하면 좀 더 쉽게 데이터를 처리할 수 있게된다.

<br/>

#### ▶ XML작성법
XML을 작성하기 위해서는 특정 규칙이 있다 <font color="orange"><태그> </태그>안에 데이터를 작성하는 방식</font>이고, <br/>
파일을 굳이 xml파일로 만들 필요는 없다. 단, <font color="orange">contentType="application/xml;으로 수정</font>을 해 줘야한다.
{% highlight ruby %} 
// XML작성예시
<chat>
    <data>
        <ip>192.168.10.61</ip>
        <port>54651</port>
        <message>안녕방구야</message>
        <time>154645123</time>
    </data>
    <data>
        <ip>192.168.10.80</ip>
        <port>546</port>
        <message>안녕하슈</message>
        <time>1543</time>
    </data>
</chat>
{% endhighlight %}

<br/>

#### ▶ XML 데이터 처리
xml파일의 데이터를 처리하기 위해서는 <font color="orange">기존 responseText로 받던 데이터를 responseXML</font>로 받아야 한다.
- this.responseXML
: xml의 데이터는 responseText가 아닌 responseXML로 불러온다.
- this.responseXML.getElementsByTagName("data");
: 해당 xml파일에 있는 태그를 객체를 배열로 가져온다.
- datas[i].getElementsByTagName("ip")[0].innerHTML);
: 불러온 배열 태그에 있는 또 다른 태그를 불러와서 해당 태그 안의 내용을 반환

{% highlight ruby %}
var xhr = new XMLHttpRequest();
xhr.open("get", "sampleXML.xml", true);
xhr.onreadystatechange = function() {
    if (this.readyState == 4) {
        window.alert(this.responseXML);
        var datas = this.responseXML.getElementsByTagName("data");
        console.log(datas.length);
        for (var i = 0; i < datas.length; i++) {
            console.log(datas[i].getElementsByTagName("ip")[0].innerHTML);
        }
    }
}
xhr.send();
{% endhighlight %}

<br/>

# ◆ JSON ( JavaScript Object Notation )
원래는 AJAX에서 XML로 응답 처리하는 것이 맞지만, XML데이터 처리보다 JSON이란 것을 이용하면 더 간단하게 데이터 처리가 가능하기 때문에 <font color="hotpink">최근에는 JSON이 많이 이용</font>되고 있다.

<br/>

#### ▶ JSON 객체 변환
JSON은 객체화 시킬 수 있는 문자열 형태의 파일형식이다. 아래의 예시를 통해 살펴보자.
- JSON.parse(문자열) 
: 해당 문자열을 형식에 맞는 타입으로 변환시켜주는 메서드
{% highlight ruby %}
var d1 = "[3,4,5,6,7]";
console.log( JSON.parse(d1) ); // [3, 4, 5, 6, 7]의 배열반환
var c = "[\"가\",\"나\"]";
console.log( JSON.parse(c) ); // ["가", "나"]의 배열반환
var t = "true";
console.log( JSON.parse(t) ); // boolean타입으로 변환된다.
{% endhighlight %}
따라서 데이터를 작성할 때 실제 프로그램이 이해할 수 있게끔 적어야 한다.

> 3,4 등의 number값 등은 그냥 써주면 되지만, 가,나 등의 문자열은 "" 또는 ''표기를 해주어야 한다.

<br/>

#### ▶ JSON 작성법
JSON도 마찬가지로 jsp파일을 contentType="application/json;로 수정해 주어야 한다.
{% highlight ruby %}
<%@ page language="java" contentType="application/json; charset=UTF-8"
    pageEncoding="UTF-8"%>
[ 
    { "name" : "홍길동" , "age" : 21, "married" : false },
    { "name" : "임꺽정" , "age" : 25, "married" : true } 
]

// 길이2인 배열에 두개의 객체가 들어가 있는 형태
{% endhighlight %}

<br/>

#### ▶ JSON불러오기
JSON파일의 데이터는 <font color="orange">responseText</font>로 불러온 후,<br/> <font color="orange">JSON.parse를 통해 객체로 변환</font>하여 사용한다.
{% highlight ruby %}
// 위 JSON파일의 모든 이름 가져오기
var xhr = new XMLHttpRequest();
xhr.open("get", "04Ajax.jsp", true);
xhr.onreadystatechange = function() {
    if (this.readyState == 4) {
        window.alert(xhr.responseText);
        var obj = JSON.parse(xhr.responseText);
        for (var i = 0; i < obj.length; i++) {
            obj[i].name
        }
    }
}
xhr.send();
{% endhighlight %}

> 반대로 스크립트객체를 json문자열 형태로 변환하는 메서드는 <font color="orange">JSON.stringfy(변환할 객체)</font>이다. <br/>
(but, 응답을 스크립트로 처리하는 경우는 거의 없으므로 사용빈도가 낮다. )

<br/>

# ◆ JSON 라이브러리 - Gson
Ajax의 응답을 하기 위해 JSON문자열을 보내 주어야 하는데, 이를 하드코딩으로 하는 경우는 거의 없기 때문에 <font color="orange">백단에서는 객체를 JSON문자열 형태로 바꿔주어야 한다.</font><br/>
이를 간편하게 제공하는 많은 라이브러리들이 있지만 그 중 대표적으로 jackson libary, gson libary가 있다.

<br/>

#### ▶ Gson 사용법
##### 1. 다운로드 => 메이븐저장소 ( mvnrepository.com) Gson.jar
##### 2. WEB-INF 라이브러리 추가
##### 3. import="com.google.gson.*";
##### 4. 객체생성 : <% Gson gson = new Gson(); %>
##### 5. JSON변환 :  gson.toJson(변수);

<br/>

#### ▶ JSON으로 변환된 언어는 모두 String 형태로 나온다.
{% highlight ruby %} 
import="com.google.gson.*";
Gson gson = new Gson();

String str = "문자열"; 
String strJson = gson.toJson(str); // "문자열"
int[] ar = new int[] { 3, 45, 65 };
String arJson = gson.toJson(ar); // [3, 45, 65]
String[] jobs = "전사,암살자,지원가,전문가".split(",");
String jobsJson = gson.toJson(jobs); // [전사, 암살자, 지원가, 전문가]
{% endhighlight %}

- 컬렉션객체들 또한 JSON형태로 변환할 수 있다.
: 단, Javascript는 컬렉션객체가 없기 때문에 적절한 객체 형태로 받아올 수 있다.<br/>
ex )  List<Map> => JSON 변환
{% highlight ruby %}
// Map은 배열에 스크립트객체를 담고있는 형태
[
    {"time":1516952581519,"addr":"192.168.10.80","port":53030,"msg":"ㅓ오런ㅇㅁㄹ"},
    {"time":1516952584958,"addr":"192.168.10.80","port":53030,"msg":"듀르바듀르바~"}
]
{% endhighlight %}

<br/>

#### ▶ JSON스트링을 다시 객체로 변환
JSON문자열을 다시 객체로 변환시키는 메서드는 <font color="orange">GSON객체.formJson(변환문자열, 받을타입.class);</font>이다.
{% highlight ruby %}
Map m = gson.fromJson(str2, Map.class);
{% endhighlight %}
str2가 JSON문자열 이라면, 위의 방법으로 Map객체로 다시 변환할 수 있다.<br/>
( 주의할 점은 해당 스트링이 Map형태가 아니라면, 오류가 터진다. )<br/>
List, VO객체 등등도 가능.

<br/>

#### ▶ 변환처리 정리
GSON이 자바객체들을 어떤형식으로 변환시키는지 정리해보자.
- 자바의 Map
: javascript object => { }
- 자바의 배열, List
: javascript의 array => [ ]
- 자바의 List<Map>
: javacript object형 array => [{ }, { }, ... ]
- GSON은 자바의 VO객체도 javascript의 object로 바꿈

<br/>

#### ▶ SQL문 JSON처리 
하나의 JSON파일에 여러 개의 SQL문을 반환 할 때는 <font color="orange">List<Map>으로 처리</Map>하여<br/>
스크립트에서 SQL문 마다 반환된 list를 반환해서 toJSON으로 처리하면 간단하게 해결할 수 있다.

<br/>

#### ▶ Gson Date객체 포맷팅
Date타입의 객체는 가공하여 사용하기 까다로운 형태로 받아와지기 때문에 Gson에서 원하는 형식의 Date타입 객체를 JSON으로 변환할 수 있도록 제공된다.

- 기본 Date타입의 JSON변환
{% highlight ruby %}
@ResponseBody
public String timeNow() {
    Date date = new Date();
    Gson gson = new Gson();
    return gson.toJson(date);
}

// => Oct 4, 2019 2:38:42 PM
{% endhighlight %}

<br/>

- GsonBuilder를 이용한 Date포맷팅
: Gsonbuilder객체를 통하여 Date형식을 포맷팅 한 후에 create()메서드를 통해 다시 Gson객체를 반환받을 수 있다.
{% highlight ruby %}
@ResponseBody
public String timeNow() {
	Date date = new Date();
	GsonBuilder gb = new GsonBuilder();
	gb.setDateFormat("yyyy/MM/dd HH:mm:ss");
	Gson gson = gb.create();
    
    return gson.toJson(date);
}

// => 2019/10/04 14:45:49
{% endhighlight %}

- Spring 등록
: 위와 같은 방식으로 Spring에서는 IOC에 등록하여 간편하게 뽑아 사용할 수도 있다.
{% highlight ruby %}
<bean class="com.google.gson.GsonBuilder" id="gsonBuilder">
	<property value="yyyy/MM/dd HH:mm" name="dateFormat" />
</bean>
<bean id="gson" factory-method="create" factory-bean="gsonBuilder" />
{% endhighlight %}


<br/>