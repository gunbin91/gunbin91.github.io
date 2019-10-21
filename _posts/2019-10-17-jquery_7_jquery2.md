---
layout: post
title: "7. Jquery(제이쿼리) - Animation 및 Ajax"
tags: [ javascript, jquery ]
date: 2019-10-17
sub_title: "Jquery"
categories: [ javascript ]
---

<p align="center">
    
</p><br/>

## ◆ Effect (Animation)
JQuery에서 제공하는 애니메이션 효과

<br/>

### ▶ hide(), show(), toggle()
객체의 display옵션을 조절하여 숨기거나 보여줌 ( none, block )
- $("#id").hide() : 해당 객체를 숨김 ( display=none )
- $("#id").show() : 해당 객체를 보여줌 ( display=block )
- $("#id").toggle() : hide()와 show()를 토글 형식으로 작동

<br/>

### ▶ fadeIn(), fadeOut, fadeToggle()
객체의 <font color="orange">opacity</font>옵션을 조절하여 서서히 숨기거나 보여줌 ( 0~1 설정가능한 <font color="orange">투명도</font> )
- $("#id").fadeIn() : 해당 객체를 보여줌 ( opacity= 0 -> 1 )
- $("#id").fadeOut() : 해당 객체를 숨김 ( opacity = 1 -> 0 )
- $("#id").fadeToggle() : fadeIn()과 fadeOut()을 토글형식으로 작동

<br/>

### ▶ slideUp(), slideDown(), slideToggle()
객체를 슬라이드 형식으로 보여주거나 숨김
- $("#id").slideUp() : 해당객체를 슬라이드 형식으로 올려서 숨김 
- $("#id").slideDown() : 해당 객체를 슬라이드 형식으로 내려서 보여줌
- $("#id").slideToggle() : slideUp()과 slideDown()을 토글형식으로 작동

> 위 세 종류의 이펙트 함수의 인자로 function(){ }를 정의해 놓으면 해당 호출이 끝난 후 <font color="orange">콜백 함수</font>로 정의한 함수가 호출된다.<br/>
ex ) $(“#id”).slideDown(function(){ window.alert(“콜백호출”); } );

<br/>

### ▶ animate()
animate는 객체의 <font color="orange">css속성변화를 서서히</font> 주는 효과로 속성을 지정 할 때는 JSON형식으로 지정한다.<br/>
또한 여러 animate를 동시에 설정이 가능하고, 순서대로 처리되며, 두 번째 인자로 function()을 등록하여 콜백 함수처리가 가능하다.
{% highlight ruby %}
$("#t").click(function() {
	$("#h").animate({
		"left" : "200px",
		"font-size" : "100px"
	}).animate({
		"opacity" : "0"
	}, function() {
		window.alert("JQUERY EFFECT");
	});
});
{% endhighlight %}

<br/>

## ◆ JQuery의 AJAX 처리
{% highlight ruby %}
$.ajax("01ajax.jsp", {
	"async" : true,
	"data" : {
		"id" : "master",
		"pass" : "1234"
	},
	"method" : "get"
}).done(function(rst) {
	window.alert(rst);
});
{% endhighlight %}

- &nbsp;<font color="orange">$.ajax( url , setting ).done(function(변수){});</font> 형식으로 AJAX를 넘긴다.
- url 
: 요청을 보낼 페이지의 주소
- setting
: 객체형식(JSON형식)으로 보내며, setting의 객체 킷값은 정해져있다.
- "async" 
: 동기/비동기 설정 (boolean)
- "data" 
: 요청페이지로 넘길 파라미터를 설정<br/>
=> 파라미터의 설정은 또 다시 객체 형식(JSON형식)으로 만들어서 보내야 한다.
- "method" 
: method방식을 설정 (“get”/“post”)
- done(function(변수){});
: done함수는 요청페이지에서 응답으로 받아온 후 작업 할 함수이며, 매개변수는 해당 요청페이지의 내용이 그대로  담겨져 있다.

## ※주의  
### ▶ 응답데이터 JQuery와 Javascript차이 
Jquery에서는 요청페이지의 contentType에 따라 다른 객체 값이 응답으로 날아오게 된다.<br/>
요청 페이지의 컨텐츠타입이 contentType="application/json; 일 때, 기존 스크립트의 Ajax처리 방식에서는 JSON.parse(responseText)로 변환해서 사용해야 하지만, <font color="orange">JQuery에서는 contentType에 따라 자동으로 변환돼서 응답이 날아오기 때문에 변환하지 않고 사용</font>한다.
- contentType="application/xml" 일때는 responseXML의 결과로 받아오게 된다. )
- 단, <font color="orange">contentType이 text/html;일 때는 똑같이 파싱</font>해서 써야한다. )

<br/>

### ▶ data의 킷값에 해당하는 value값들을 배열로 보낼 때,( ex) "front" : [ "a", "b", "c" ] )
주소창의 키의 문자열은 [ ] 가 붙어서 날아가게 된다. ( ex ) .jsp?front[]=a&front[]=b... )
따라서 배열데이터를 뽑아낼 때는 request.getParameterValues("front[]") 로 뽑아야한다.
단, 애초부터 "front[]"로 킷값을 잡게 된다면, 자동적으로 []가 붙지 않는다.

## ◆ AJAX 단순처리
: $.ajax() 방식을 get, post 방식에 따라 좀 더 단순, 편리하게 처리할 수 있다.
▶ get방식 ajax요청
$("#t1").on("click", function() {
$.get("02ajax.jsp", {
"word" : "ajax",
"front" : [ "java", "jsp", "css", "jquery" ]
}, function(rst) {
window.alert("rst = " + rst);
});
});
- 형식 : $.get( url, data, callbackFunction ); 
: 위의 형식으로 get방식의 요청을 .ajax대신 .get으로 보낼 수 있다.
( data부분은 $.ajax()방식에서 "data"를 처리할 때와 같은 형식으로 한다. )

▶ post방식 ajax요청
: get방식과 똑같이 작성하며, $.post만 달라진다.





<br/>