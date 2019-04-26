---
layout: post
title: "3. 개발이론"
tags: [ java ]
date: 2019-04-26
categories: [ java ]
---

<p align="center">
    대부분의 개발자들은 같은 시간에 많은 작업을 하길 원하고, 한번 만들어둔 프로그램을 쉽게 유지/보수 할 수 있게 되기를 원한다. 이를 쉽게 할 수 있도록 하는 개념이 자바에서 사용하는 <font color="hotpink">객체지향 프로그램밍(Object-oriented programming)</font>이다.
</p><br/>

# ◆ 프로그램 개발 론
 - 절차 지향 ( procedure 중심의 언어 )- Procedural Programming
 - ★객체 지향 ( Object 중심의 언어 )- Object Oriented Programming
 - 관점 지향 ( Aspect 중심의 언어 )- Aspect Oriented Programming
<br/>
=> 현재 쓰이고 있는 프로그래밍 언어들은, 모두 3개중에 포함이 되어있다. 
자바는 객체 기반의 프로그래밍 언어이다.
<br/>  
=> 객체지향 프로그래밍 기법을 익히려면, 절차 지향 프로그래밍 기법에 대해 먼저 살펴보는 것이 좋다.

<br/><br/>

# ◆ 절차적(not순차) 프로그래밍( procedural programming) 
Procedure = 순서, 프로그래밍 단위 작업 = 함수 또는 서브루틴<br/>
(단위 작업 하나 하나를 프로시저라고 통칭, C언어에서는“함수”, 자바에서는“메소드”)
<br/>
(언어마다 부르는 용어가 조금씩 다를 수 있다. ) 

<br/><br/>

# ◆ 오버로딩 (Overloading )
매개변수의 <font color="orange">자료형(Type) 또는 개수가 다른 같은 이름을 가진 메서드</font>를 만드는 것.
<br/>
cf ) System.out.println()메서드는 String뿐만 아니라 다른 자료형의 데이터도 모두 출력 가능. 
<br/>
=> println의 인자로 들어오는 매개변수들에 대한 오버로딩을 해놓았기 때문에 가능.
<br/>
( 오버로딩이 가능한 메서드는 다른 메서드로 취급하기 때문에 return 자료형이 달라져도 상관없음 )
<br/>
{% highlight ruby %}
public String A(int a){} 
public int A(double a){} 
public int A(double a, double b){}
{% endhighlight %}
등과 같이 같은 이름으로 여러개의 메서드를 오버로딩 할 수 있다.



<br/>