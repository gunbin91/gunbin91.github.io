---
layout: post
title: "객체/배열 합치기 - $.extend()/$.merge()"
tags: [ javascript, jquery, extend ]
date: 2019-12-09
sub_title: "Jquery"
categories: [ javascript ]
---

<p align="center">
    
</p><br/>

## ◆ 객체 합치기 - $.extend()
자바스크립트의 두개의 객체를 합치는 방법 중 Jquery에서 제공되는 $.extend()메서드가 있다.<br/> <font color="orange">$.extend(obj1, obj2)</font>를 호출하게 되면, <font color="orange">obj1객체는 obj1과 obj2가 합쳐진 값으로 변환</font>된다. 또한 중복되는 객체값은 덮어씌워지게 된다.

{% highlight ruby %}
var obj1 = {a: 100, b:200};
var obj2 = {c: 300, d:400};
$.extend(obj1, obj2);
console.log(obj1);
console.log(obj2);

// 결과
// {a: 100, b:200, c: 300, d:400}
// {c: 300, d: 400}

// 중복값이 있을 때
var obj3 = {a: 100, b:200};
var obj4 = {b: 300, c:400};
$.extend(obj3, obj4);
console.log(obj3);
console.log(obj4);

//결과
// {a: 100, b: 300, c: 400}
// {b: 300, c: 400}
{% endhighlight %}

<br/>

## ◆ 배열 합치기 - $.merge()
$.extend()와 마찬가지로 배열 객체도 합칠 수 있는 메서드가 있다.<br/> <font color="orange">$.merge(arr1, arr2)를 호출하게 되면 arr1은 arr1과 arr2가 합쳐진 값으로 변환</font>된다. 단, $.merge는 중복값을 제거하지 않는다.

{% highlight ruby %}
var arr1 = [ 1, 3 ];
var arr2 = [ 3, 4 ];
$.merge(arr1, arr2)
console.log(arr1);
console.log(arr2);

// 결과
[ 1, 3, 3, 4 ]
[ 3, 4 ]
{% endhighlight %}


<br/>