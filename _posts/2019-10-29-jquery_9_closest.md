---
layout: post
title: "상위 객체 제어 - parents VS closest "
tags: [ javascript, jquery, closest, parents ]
date: 2019-10-29
sub_title: "Jquery"
categories: [ javascript ]
---

<p align="center">
    부모 객체태그를 jquery의 선택자로 선택하는 방법
</p><br/>

## ◆ closest() vs parents()
두개의 메서드 모두 <font color="orange">부모객체를 반환</font>해 주는 메서드이다.<br/>
( 부모객체의 형제태그 까지는 찾지 않음 )

<br/>

### ▶ closest() vs parents() 차이
- parents()
: 인자에 해당 하는 <font color="orange">모든 부모레벨의 객체를 배열</font>로 담아온다.따라서, 해당 부모객체 전체가 제어된다. ( 단 출력은 [0]인덱스의 객체를 출력하게 된다. )

<br/>

- closest()
: 인자에 해당하는 제일 가까운 <font color="orange">부모객체만 반환</font>된다. 따라서 바로 위 부모객체만을 제어할 수 있다.

{% highlight ruby %}
<span class="level1"></span>
<span class="level2"> 
	<span class="level3"> 
		<a id="a"></a>
	</span>
</span>

<script>
// 반환은 같음
console.log($("#a").parents("span")); => level3 반환
console.log($("#a").closest("span")); => level3 반환

// level3, level2 모두 배경색 변경
$("#a").parents("div").css("background","yellow");
// level3만 배경색 변경
$("#a").closest("div").css("background","yellow");
</script>
{% endhighlight %}


<br/>