---
layout: post
title: "6. Jquery(제이쿼리) - 연동 및 객체제어"
tags: [ javascript, jquery ]
date: 2019-07-01
sub_title: "Jquery"
categories: [ javascript ]
---

<p align="center">
    Jquery는 javascript를 좀 더 편리하게 사용할 수 있도록 지원해주는 라이브러리다.
</p><br/>

## ◆ 제이쿼리 ( JQuery )
자바스크립트를 조금 더 편하게 사용할 수 있는 프론트엔드 기술 ( 언어 )<br/>
jQuery는 HTML의 클라이언트 사이드 조작을 단순화 하도록 설계된 크로스 플랫폼의 자바스크립트 라이브러리다. 

<br/>

## ◆ 연동 방식
JQuery를 연동하는 방식에는 두 가지 방식이 있다.<br/>
( Jquery는 보통 <head>태그 안에서 연동시켜 놓는다. )

<br/>

#### ▶ 프로젝트에 직접 포함시키는 방식 
https://jquery.com/ 접속 후 .js파일을 직접 다운 후 WebContent아래에 js폴더를 따로 만들어서 .js파일을 복사, jsp파일에서  .js파일이 있는 경로로 스크립트 src를 연동시켜 놓는다.
{% highlight ruby %}
<script src="js/jquery-3.3.1.min.js"></script>
// 절대경로일 경우 수정한 경로부터..
{% endhighlight %}

<br/>

#### ▶ CDN 방식
https://jquery.com/ 접속하여 다운로드 페이지에 CDN방식에 대한 설명이 있다.<br/>
해당 방식은 직접 .js파일을 포함하지 않아도 인터넷으로 접속하여 불러올 수 있게 된다.
{% highlight ruby %}
<script
src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
{% endhighlight %}

<br/>

▶ 예시
{% highlight ruby %}
<script src="js/jquery-3.3.1.min.js"></script>

<button type="button" id="btn">JQUERY</button>
<script>
$("#btn").click(function() {
    window.alert("btn Click");
});
</script>
// $("#btn") : 버튼의 아이디로 객체를 찾는다.
// .click(function(){}); : 해당 버튼의 onclick메서드를 등록
{% endhighlight %}

<br/>

## ◆ Element탐색
javascript에서 Element 탐색은 id(1) /className(Array) /tagName(Array) /name(Array)만 지원하지만, JQuery는 다양한 형태로 지원한다.<br/>
( 물론, JQuery에서도 javascript에서 지원하는 기본적인 탐색은 모두 지원한다. )

<br/>

#### ▶ $( ) 
JQuery객체로 변환하기 위해 사용하는 키워드로, 괄호 안 문자열에 따라 id, class .. 등이 달라진다. <br/>
- <font color="orange">$()로 묶여서 JQuery객체로 변환되어야지만 JQuery의 문법을 쓸 수 있다.</font>
- this또한 $(this) 형태로 묶어 주어야 JQuery문법을 쓸 수 있다.
- JQuery로 변환된 객체는 script의 문법이 먹히지 않고, JQuery의 문법으로 사용해야 한다. <br/>
( 반대의 경우도 마찬가지 )

<br/>

- id로 찾기
: id로 찾을 때는 앞에 <font color="orange">#</font>을 붙여서 찾는다.(= getElementById )
{% highlight ruby %}
$("#keyword") // id="keyword"라는 아이디를 가진 객체를 찾아내 jqeury객체로 반환
// script: getElementById("keyword")
{% endhighlight %}

<br/>

- class로 찾기
: class로 찾을 때는 앞에 <font color="orange">.</font>을 붙여서 찾는다. (= getElementsByClass )
{% highlight ruby %}
$(".ar") // class="ar" 을 가진 객체를 찾아내 jquery객체로 반환.
// script: getByElementsByClass("ar")
{% endhighlight %}

<br/>

- tag로 찾기
: 태그로 찾을 때는 <font color="orange">태그명만</font> 써준다. (= getElementsbyTag )
{% highlight ruby %}
$("p") // <p>태그를 가진 객체를 찾아낸다.
// script: getElementsbyTag("p")
{% endhighlight %}
 
<br/>
 
## ◆ JQuery의 특징

#### ▶ 일괄제어
javascript에서 class등의 배열로 반환되는 객체들의 메서드를 등록시킬 때,반복문을 돌리면서 일일이 function을 등록시켜 줘야하지만, JQuery에서는 한 번에 등록이 가능하다. ( 일괄제어 가능 )
{% highlight ruby %}
$(“.class”).click(function(){ 
    console.log(“메서드등록”); });
{% endhighlight %}

<br/>

#### ▶ javascript로 반환된 객체도 $()으로 묶어서 JQuery객체로 사용할 수 있다.
{% highlight ruby %}
$(document.getElementById("id")).click(function(){}); 
{% endhighlight %}

> 즉, $(“#id”)괄호 안에 "#id"는 getElementById("id")와 같은 역할을 하지만 $() 안에서 선언되지 않는다면 의미가 없어진다.

<br/>

## ◆ Filtering
JQuery는 <font color="orange">객체탐색과 동시에 조건(filtering)</font>을 설정해서 객체를 얻어낼 수 있다.<br/>
필터링은 $(“#id”)등의 단일 객체일 때는 의미가 없고, $(“.class”)등의 <font color="orange">묶여있는 객체일 경우에만 의미가 있다.</font>
- 조합방식은 <font color="orange">$(" 기본 : 필터링 ")</font>의 형태 

<br/>

#### ▶ 필터링 조건
자주 쓰이는 필터링 조건은 :first / :last / :even / :odd / :enabled / :disabled / :selected / :checked 등이 있다.
<br/>
#### ▶ 필터링으로 객체 뽑아내기
- $(".item:first") : 첫번째 객체만 뽑아낸다.
- $(".item:last") : 마지막 객체만 뽑아낸다.
- $(".item:even") : 짝수 객체만 뽑아낸다. ( 인덱스는 0번부터 시작 )
- $(".item:odd") : 홀수 객체만 뽑아낸다.
- $(".item:enabled") : enabled된 객체만 뽑아낸다.
- $(".item:disabled") : disabled된 객체만 뽑아낸다.
- $(".item:selected") : selected된 객체만 뽑아낸다.
- $(".item:checked") : checked된 객체만 뽑아낸다.
- 이렇게 필터링으로 걸러져 나온 객체들을 일괄 제어 할 수는 있지만, 하나하나씩 처리하기 위해서는 다른 방법이 필요하다.

<br/>

## ◆ JQuery제어
JQuery의 HTML제어는 메서드의 형태로 되어있고, <font color="orange">인자가 없을 경우 해당 옵션의 값을 반환</font>하고, <font color="orange">인자가 있을 경우 변환</font>한다.<br/>

또한, 객체가 여러 개일 경우 값을 설정하는 것은 모두 적용되지만, 
반환되는 것은 첫 번째 객체의 것만 반환된다.

<br/>

#### ▶ onclick메서드 제어
{% highlight ruby %}
$("#id").click(function(){});
// == getElementById("id").onclick=function(){}
{% endhighlight %}
( 대부분의 on메서드는 JQuery에서 on을 뺀 이름으로 사용 ( onchange => change )<br/>
=> on메서드도 마찬가지로 인자가 없을 경우 해당 메서드를 반환하여 호출하게 된다.

<br/>

#### ▶ innerHTML제어
{% highlight ruby %}
$("#id").html("html"); 
// (자바스크립트)== .innerHTML = "html"
{% endhighlight %}

<br/>

#### ▶ value제어
{% highlight ruby %}
$("#id").val("어쩌구");
// (자바스크립트)== .value = "어쩌구"
{% endhighlight %}

<br/>

#### ▶ 태그 속성 제어
문자열 값을 가지고 있는 태그의 옵션들을 <font color="orange">attr을 통해 제어</font>하게 된다.
{% highlight ruby %}
$("#id").attr("type", "radio") 
// (자바스크립트) == .type="radio" 
{% endhighlight %}

<br/>

#### ▶ boolean속성제어 ( disabled / checked / selected )
문자열이 아닌 <font color="orange">boolean속성을 가지고 있는 속성값</font>들은 attr이 아닌 <font color="orange">prop를 통해 제어</font>할 수 있다.
{% highlight ruby %}
$("#id").prop("checked", false); 
// !$("id").prop("checked"); ( 앞에 !(not)를 붙이면 반대의 결과가 나옴 )
{% endhighlight %}

<br/>

#### ▶ 태그 속성 제거
{% highlight ruby %}
$("#id").removeAttr("속성");
// 해당 속성에 해당하는 값을 제거
{% endhighlight %}

<br/>

#### ▶ style속성 제어
자바스크립트에서는 style속성을 타고 들어가지만, JQuery에서 style옵션의 제어는 css()메서드를 통해 제어하게 된다.
{% highlight ruby %}
$("#id").css("color","red"); 
// (자바스크립트) == .style.color="red" ( css는 style속성 변환시 사용 )
{% endhighlight %}

<br/>

#### ▶ class추가
{% highlight ruby %}
$("#id").addClass("class");
== $("id").attr("class",$("id").attr("class") + " class");
// class옵션은 string값이기 때문에 string을 추가함으로서 추가도 가능
{% endhighlight %}

<br/>

#### ▶ class제거
{% highlight ruby %}
$("#id").removeClass("c1");
{% endhighlight %}

<br/>

#### ▶ get
{% highlight ruby %}
$(".clss").get(숫자);
{% endhighlight %}
여러 개의 객체 중에서 해당 인덱스에 해당하는 객체를 반환<br/>
=> 반환되는 객체는 스크립트용 객체이기 때문에 다시 JQuery로 제어하기 위해서는
반환된 객체를 $()로 다시 묶어서 사용해야 한다.

- $(".class").length : 해당 객체가 여러 개일 때 개수 반환
- $(".class").index() : 해당 객체가 클래스 안에서 몇 번째 객체인지를 반환<br/>
( 중간에 개행태그 등의 태그가 있을 경우 br도 포함해서 체크하기 때문에 크게 사용할 일은 없다. ) 

<br/>

## ◆ 이벤트처리
on메서드를 등록/제어하는 방식에는 두 가지가 있다.

#### 1. $("#id").click(function(){});
{% highlight ruby %} 
$("#b1").dblclick(function() {
    window.alert("b1");
}).onmouseover(function(){
    window.alert("b11");
});
{% endhighlight %}

<br/>

#### 2. $("#id").on("click",function(){});
{% highlight ruby %} 
$("#b2").on("click", function() {
    window.alert("b2");
}).on("mouseleave", function() {
    window.alert("b22");
})
{% endhighlight %}

- 두 가지 방식 모두 자신의 객체를 반환하기 때문에 연속해서 메서드 등록이 가능하다.

<br/>

#### ▶ each
{% highlight ruby %}
$(“.class”).each(function(){});

$(".class : checked").each(function(){
    window.alert($(this).val()); 
});
{% endhighlight %}
해당 클래스에 해당되는 객체들이 특정 함수가 작동되게 유도<br/>
( <font color="orange">함수 선언과 동시에 작동</font>될 수 있도록 할 수 있게 하는 기능 )<br>
보통의 경우 여러 개가 반환되는 객체의 경우에 대부분 사용한다.<br/>

- $(“.class”)로 객체들을 뽑아낼 때, 등록 및 제어 등이 모두 일괄처리 되기 때문에 하나씩 뽑아서 사용하기 어렵다.<br/>
따라서 <font color="orange">여러 개로 묶여있는 객체들 각각에 대한 제어가 필요할 때</font>, each()메서드를 이용하여 객체들에 대한 정보들을 뽑아서 저장해 놓거나, 제어할 수 있다.<br/>
- 또한, each는 함수 등록과 동시에 강제 호출이 되기 때문에, 보통 on메서드 계열 메서드 안에서 작성한다.

<br/>

#### ▶ 트리거(trigger)
트리거는 해당 이름의 함수를 <font color="orange">강제 호출시키는 메서드</font>로, 트리거의 인자로 들어올 수 있는 메서드 이름은 <font color="orange">on계열 등의 이름이 정해진 메서드뿐</font>이다.<br/>
{% highlight ruby %}
$("#bt2").click(function() {
    $("#t").trigger("change");
});
{% endhighlight %}
- 다른 객체에서 똑같은 메서드를 사용해야 할 때 보통 많이 사용되며, $(“#id”).click()안에 바로 트리거 함수를 등록시킬 시 그냥 호출이 되기 때문에<br/>
등록을 할 때에는 function(){ }안에서 호출하도록 해야 한다.<br/>
(즉 function(){$("#id").trigger("메서드")}의 형태로 하나의 등록 함수 형태로 만드는 것이다. )

- 트리거는 강제 호출이기 때문에 $("#t").trigger("change");는 $("#t").change()와 같은 역할을 한다. (또는 같음)<br/>
( 둘 다 호출 기능 이지만, function(){} 안에 선언할 시 하나의 함수가 만들어진다. )


따라서 아래도 가능
{% highlight ruby %}
$("#bt2").click(function() {
$("#t").change();
});
{% endhighlight %}

<br/>

## ◆ 그 외
- css 에서도 JQuery와 같은 처리를 하기 때문에 #은 id, .은 class 등등으로 처리한다.
{% highlight ruby %}
.mode{
 font-size:50px;
} 
<div class="mode">
{% endhighlight %}




<br/>