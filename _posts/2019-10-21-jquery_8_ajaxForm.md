---
layout: post
title: "8. form데이터 Ajax요청( serialize() )"
tags: [ javascript, jquery, serialize ]
date: 2019-10-21
sub_title: "Jquery"
categories: [ javascript ]
---

<p align="center">
    form데이터를 submit하지 않고, ajax요청으로 보내는 방법을 알아보자.
</p><br/>

## ◆ from데이터 Ajax로 보내기
form의 기본 동작인 action경로로의 submit은 자동으로 render()라는 메서드가 호출되기 때문이다. Ajax로 파라미터를 보내기 위해서는 해당 메서드 호출을 막는 방법이 필요하다.

<br/>

### ▶ submit막기
form태그 안에 버튼이 하나 있을 경우, type이 submit이 아니더라도 form데이터를 submit하게된다.
<br/>따라서 Ajax로 파라미터를 보내기 위해서는 이 submit을 막는 작업이 필요하다. 
<br/>여러 방법이 있겠지만 대표적인 2가지를 알아보자.

#### 1. return false
submit버튼의 onclick이벤트나 form의 onsubmit이벤트가 <font color="orange">false를 리턴하게 되면 submit을 하지 않게 된다.</font>
{% highlight ruby %}
$("#subbt").unbind("click").click(function(event){
	// ajax작업
	return false;
});
{% endhighlight %}

<br/>

#### 2. event.preventDefault()
DOM이벤트(on메서드)의 인자인 <font color="orange">이벤트객체의 prevenDefault() 메서드는 이벤트의 기본 동작을 중단</font>시키기 때문에 submit이 발생하지 않는다.
{% highlight ruby %}
$("#subbt").unbind("click").click(function(event){
	event.preventDefault();
	// ajax작업
});
{% endhighlight %}

<br/>

### ▶ form데이터 묶어서 보내기( serialize() )
form데이터를 Ajax로 보내기 위해서는 각각의 input객체의 value값을 뽑아내야 한다.<br/>
하지만 입력 데이터가 많아질 경우 해당 방법은 매우 까다로워지기 때문에 jquery는 <font color="orange">form데이터를 한번에 추출할 수 있는 메서드인 serialize()</font>를 지원한다.
{% highlight ruby %}
<form id="form1">
	a <input type="text" name="a" /><br /> 
	b <input type="text" name="b"></input/><br />
	c <input type="text" name="c" /><br />
	<button id="subbt">확인</button>
</form>

<script>
$("#subbt").unbind("click").click(function(event){
	event.preventDefault();
	console.log( $("#form1").serialize());
	// a=""&b=""&c="" 형식으로 반환해준다.
});
</script>
{% endhighlight %}



<br/>