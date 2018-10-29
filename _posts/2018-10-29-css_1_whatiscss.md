---
layout: post
title: "1. CSS ?"
tags: [ css ]
date: 2018-10-29
categories: [ css ]
---

<p align="center">
html언어에도 여러가지 옵션들이 존재하여 모양이나 컬러등을 변경할 수 있지만,<br/> 순수html만으로는 디자인적인 요소들을 세밀하게 조작할 수 없다.<br/> 따라서 html의 디자인적인 요소를 적용시켜 줄 수 있는 CSS가 있다.
</p><br/>

# CSS ( Cascading Style Sheet )
정보를 표현하는 HTML의 기능을 디자인적 요소 없이 정보에만 집중될 수 있도록 디자인적인 면은 분리되도록 만든 언어 즉, HTML의 <font color="deeppink">디자인적인 요소를 담당하는 언어</font>이다.

<br/><br/>

# CSS적용 방법
css적용 방법에는 크게 세 가지 방법이 있다.

### 1. 태그 안에 style속성으로 적용시킨다.
ex )&nbsp;&nbsp; &lt;h1 <font color="orange">style</font>="color:red;">

### 2. &lt;style>태그 안에 선언해 둔다.
ex )&nbsp;&nbsp; <font color="orange">&lt;style></font> h2{ color:blue; } <font color="orange">&lt;/style></font> 

### 3. 따로 .css확장자로 만들어 link태그로 html에 포함시킨다.
ex )&nbsp;&nbsp; &lt;<font color="orange">link</font> rel="stylesheet" href="static/style.css">

<br/><br/>

# CSS 속성의 구분은 세미콜론(;)으로 한다.
ex )&nbsp;&nbsp; style="color:red<font color="orange">;</font> align=left<font color="orange">;</font>"

> 태그에 style옵션을 이용하는 것이 아닌 따로 빼두어 적용시킬 때는 "선택자{ 옵션명:값; }"의 문법을 따른다.

<br/>