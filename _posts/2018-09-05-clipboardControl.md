---
layout: post
title: "Javascript 클립보드 제어( 자동 출처 삽입 )"
tags: [ etc, javascript, clipboard ]
date: 2018-09-05
categories: [ etc ]
---

<p align="center">
    블로그등에서 포스터를 복사할 때 자동으로 출처가 따라오는것을 본적이 있을것이다.<br/>
    기본적으로 복사한 글들은 운영체제 안의 작은 메모리에 해당하는 '클립보드'라는 곳으로 저장되는데 이 클립보드를 제어하여 복사방지 및 수정이 가능하도록 할 수 있다.
</p><br/>

# IE(Internet Explorer)
클립보드를 제어하고자 하는 영역에 복사할 때 호출되는 <font color="deeppink">onCopy</font>메서드를 이용하여 스크립트 함수를 통해 제어할 수 있다.
<br/><font color="orange">window.clipboardData.getData('Text')</font>를 이용하여 클립보드에 복사된 내용을 불러올 수 있고, <font color="orange">window.clipboardData.setData('Text','수정내용')</font>을 이용하여 클립보드에 복사된 내용을 수정할 수 있다.


{% highlight ruby %}
<div id="contents_area" onCopy="javascript:copy_test();">
이곳을 드래그하여 복사한 후 붙여넣기 하십시오.
</div>

<script>
function copy_test()
    {
        if (window.event)
        {
            window.event.returnValue = true;
            window.setTimeout('copy_t()', 25);
        }
    }
    
function copy_t()
{
    if (window.clipboardData)
    {
        var txt = window.clipboardData.getData('Text'); // 클립보드 내용 가져오기
        var retUrl = document.URL; // 페이지 url
        txt = txt +'출처 :'+retUrl;
        var result = window.clipboardData.setData('Text', txt); // 클립보드 내용 수정하기
    }
}
</script>
{% endhighlight %}

> 단, 위 코드는 <font color="red">IE에서만 적용이 가능하다.</font> Chrome브라우저 같은 경우 보안상의 이유로 window.clipboardData를 사용할 수 없게 해놓았기 때문이다. 

## Chrome
크롬 또는 다른 브라우저에서는 조금 다른 방식으로 접근이 가능하다.<br/><font color="orange">window.addEventListener('copy')</font>를 이용하여 해당 타이밍에 한번의 수정할 기회가 생기게 되는데, window객체가 아닌 이벤트 객체를 이용하여 클립보드를 수정할 수 있다.

{% highlight ruby %}
<script>
window.addEventListener('copy', function (e){
     document.execCommand('copy');
     var retUrl = document.URL;
     e.preventDefault();
     e.clipboardData.setData('text/plain', document.getSelection() + 
                             "\n\n[출처]"+retUrl+"  [gunbin91 Blog]");
}, false)
</script>
{% endhighlight %}

> 위 <font color="red">리스너 메서드에서는 e.clipboardData.getData('Text')를 통해 클립보드의 내용을 불러올 수 없다.</font> 이유는 클립보드에 복사시킬 메서드를 리스너로 가로챘기 때문이다.<br/>
따라서 드래그한 내용을 가져오기 위해 <font color="orange">document.getSelection()</font>메서드를 사용하였다.

<br/>
<hr/>