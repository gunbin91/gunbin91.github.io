---
layout: post
title: "라이브러리 및 이벤트 충돌방지 - unbind"
tags: [ javascript, jquery, closest, parents ]
date: 2019-10-29
sub_title: "Jquery"
categories: [ javascript ]
---

<p align="center">
    
</p><br/>

## ◆ (function($){ })(jQuery); 형태
Jquery를 사용할 때 <font color="orange">$의 기능을 Jquery에서만 사용하도록 하는 형태</font>로, 이 안에서의 코드 작성은 단순히 Jquery코드의 작성이지만, prototype.js등과의 $충돌을 방지하기 위해 사용한다.

{% highlight ruby %}
(function($) {
    // Jquery코드작성
	console.log("Jquery call");
})(jQuery)

=> 단순 콘솔호출
{% endhighlight %}

<br/>

## ◆ DOM이벤트 재정의

- .unbind("click", function(event){});
: 기존 클릭함수를 호출하지 않고 재정의

- .bind("click", function(event){});
: 기존 클릭함수가 호출될 때 같이 호출될 메서드 정의

- .trigger("click")
: 이벤트 강제 호출
<br/>