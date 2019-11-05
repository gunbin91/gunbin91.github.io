---
layout: post
title: "Ajax-HTML(JSP)페이지 응답 제어"
tags: [ jquery, ajax, 페이지 ajax, 가상태그 ]
date: 2019-10-21
sub_title: "Jquery"
categories: [ javascript ]
---

<p align="center">
    Ajax의 응답은 보통 JSON형태로 받아와 변환하여 사용하지만, html이나 jsp페이지 자체를 응답으로 받는 경우가 발생할 수 있다. 이 때 태그를 제어할 수 있느 방법에 대해 알아보자.
</p><br/>

## ◆ JSP(or html) Ajax응답 페이지에서 특정 요소 찾는법
Ajax를 통하여 태그가 있는 Jsp나 html을 불러오게 될 경우 JSON.parse등을 사용할 수 없고,
불러온 응답 페이지는 현재 페이지가 아니기 때문에 단순히 id나 class를 통하여 객체를 가져올 수 없다.<br/>따라서 <font color="hotpink">가상의 태그 객체를 응답페이지와 결합하여 객체를 찾아가는 방식</font>으로 사용한다.

<br/>
### ▶ Jquery 셀렉터를 이용하여 가상 태그객체 생성
Jquery는 셀렉터를 통하여 특정 태그 객체를 찾는것 뿐만 아니라 특정한 태그 객체를 만들어낼 수 있다.<br/>
ex) <font color="orange">$("<div></div>");</font><br/>
위 처럼 Jquery셀렉터를 태그를 이용해 만들게 되면 해당 태그를 찾는 것이 아니라 <font color="orange">현재 페이지에 추가 되지 않은 가상의 해당 태그 객체</font>로 만들어준다.

<br/>

### ▶ 응답 페이지 제어
위 처럼 가상의 태그 객체를 만든 후 append(data)메서드를 이용하여 가상의 태그안에 ajax를 통해 불러들인 페이지를 추가해 준다.
<br/><font color="orange">append()메서드는 또 다시 해당 Jquery객체로 반환되기 때문에 find("#id")등의 메서드를 통해 객체를 제어</font>할 수 있게 된다.

{% highlight ruby %}
$.ajax({
        url: '/test.do',
        type: 'post',
        dataType: 'text',
        data: {
        	i_sEventcd: eventCd 
        },
        async: true,
        success: function(data) {
        	var result = $('<div />').append(data).find('#comment').html();
	        $("body").append(result);
        } 
});

/* ex) data =
<html>
    <body>
        <div id="comment">
            <ul>
                <li>1</li>
                <li>2</li>
                <li>3</li>
            </ul>
        </div>
    </body>
</html>
일 때, body에 <ul>~</ul>이 추가된다.
*/
{% endhighlight %}






<br/>
<hr/>