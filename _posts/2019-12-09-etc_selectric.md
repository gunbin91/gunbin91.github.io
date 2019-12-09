---
layout: post
title: "SelectBox 라이브러리 - selectric"
tags: [ etc, selectric ]
date: 2019-12-09
categories: [ etc ]
---

<p align="center">
    못생긴 select box를 꾸며주는 라이브러리 selectric 사용 법
</p><br/>
    
## ◆ selectric
select박스를 꾸며주는 라이브러리다.

<br/>

### ▶ 라이브러리 다운로드
<a href="http://selectric.js.org/index.html" target="_blank">http://selectric.js.org/index.html</a> 해당 홈페이지에서 기본적인 사용방법과 다양한 활용법에 대해 익힐 수 있다. 기본적으로 selectric을 사용하기 위해서는 아래 css, js 두 개의 파일이 필요하다.

- css 
: Demos -> 오른쪽 상단 맘에 드는 테마 선택 후 Download Css 클릭 ( <font color="orange">selectric.css</font> )
- js
: Download(ZIP)다운로드 후 /src/<font color="orange">jquery.selectric.js</font>

<br/>

### ▶ 사용
- jquery 
: {% highlight ruby %}
<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.12.4/jquery.min.js"></script>
{% endhighlight %}
- js 
: {% highlight ruby %}
<script src="jquery.selectric.js"></script>
{% endhighlight %}
- css 
: {% highlight ruby %}
<link rel="stylesheet" href="selectric.css">
{% endhighlight %}
- Using
: {% highlight ruby %}
<select>
    <option>One</option>
    <option>Two</option>
    <option>Three</option>
    <option>Four</option>
    <option>Five</option>
</select>

<script>
$(function() {
  $('select').selectric();
});
</script>
{% endhighlight %}

<br/>

<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.12.4/jquery.min.js"></script>

<link rel="stylesheet" href="/assets/css/lib/selectric.css"/>

<script src="/assets/js/lib/jquery.selectric.js"></script>

### ▶ Result

<select>
    <option>One</option>
    <option>Two</option>
    <option>Three</option>
    <option>Four</option>
    <option>Five</option>
</select>

<script>
$(function() {
  $('select').selectric();
});
</script>


<br/>
<hr/>