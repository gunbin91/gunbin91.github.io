---
layout: post
title: "4. 캐스캐이딩(cascading) - 적용우선순위"
tags: [ css,  cascading ]
date: 2018-10-29
categories: [ css ]
---

<p align="center">
    CSS는 CascadingStyleSheet의 약자인 만큼 캐스캐이딩을 제대로 알아야 css를 좀 더 꼬이지 않고 쉽게 사용할 수 있다.
</p><br/>

# Cascading
CSS(Cascading Style Sheet)약자의 앞 문자인 Cascading는 하나의 동일한 css요소가 하나의 객체에 포함되어 있을 때 어떤 css속성을 적용할 지 결정하는 <font color="deeppink">CSS우선순위 결정 규칙</font>이다.

<br/><br/>

# CSS 적용 우선순위
#### 1. 태그에 직접적으로 style속성으로 지정
#### 2. id선택자로 지정
#### 3. class선택자로 지정
#### 4. 태그선택자로 지정

> 우선순위가 동급일 때는 나중에 적용한 CSS가 우선순위가
높기 때문에 우선순위를 높이고 싶은것을 아래로 놓는다.

<br/><br/> 

# 우선순위 높이기 ( !important )
CSS속성에 "<font color="orange">!important</font>"를 키워드를 적게되면 우선순위가 최상위가 된어 해당 속성이 적용된다.<br/> 단, 이렇게 우선순위를 강제로 높이는 것은 최소한으로 사용하는 것이 좋다<br/>
<b>Ex ) li{ color:red; <font color="orange">!important;</font> }</b>


<br/>