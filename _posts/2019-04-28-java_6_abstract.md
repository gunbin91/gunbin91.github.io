---
layout: post
title: "6. 추상클래스, 객체비교 및 분기처리"
tags: [ java, abstractclass, compareto ]
date: 2019-04-28
categories: [ java ]
---

<p align="center">
    생성의 용도가 아닌 지침서 정도의 용도로 사용하는 생성불가능한 클래스인 추상 클래스에 대해 알아보자.
</p><br/>

# ◆ abstract(추상) 클래스
클래스 앞에 <font color="orange">abstract 키워드를 붙이면 추상클래스</font>가 된다. 

- 추상클래스는 기본적으로 <font color="orange">객체생성이 불가능</font>하다.( 변수는 선언은 가능 ) 
{% highlight ruby %}
public abstract class Piece{}
Piece p;=> 가능(o)
p=new Piece()=> 불가능(x)
{% endhighlight %}
객체 설계의 목적이 아닌 하위 클래스들의 제어용으로 쓰이는 클래스는 abstract class 로 만드는 것이 좋다.

#### ▶ 추상클래스 설계예제
{% highlight ruby %}
public abstract class Abclass{
    public Int a;
    
    // 오버라이드가 필수가 아님
    public void abMethod(){
		System.out.println(“추상클래스 일반메서드”);
    }
    
    // 추상 메서드는 오버라이드가 필수
    public abstract void abstMethod(){
	   System.out.println(“반드시 오버라이드 해야하는 메서드”);
    }
}
{% endhighlight %}

<br/>

# ◆ abstract method ( 추상 메서드 )
추상클래스 안에서 쓰이는 <font color="hotpink">오버라이드가 목적인 메서드</font> 또한 abstract를 붙여서 추상메서드로 만든다.
<br/>

#### ▶ 추상메서드 설계 
<font color="orange">중괄호( {} )가 없고 끝에 세미콜론( ; )을 붙인 형태</font>.
{% highlight ruby %}
public abstract boolean movableTo(int tx, int ty);
{% endhighlight %}
추상클래스를 상속받아 사용하는 클래스들은 <font color="orange">반드시 추상메서드를 오버라이드</font> 구현해 야한다.<br/>
( 추상 클래스가 추상메서드를 꼭 만들 필요는 없음 )

<br/><br/>

# ◆ super 와 this 키워드
- <b>super</b>: 부모클래스를 지칭하는 키워드 <br/>
=> super() : 부모생성자 호출, super.필드 : 부모의 필드

- <b>this</b>: 해당 클래스를 지칭하는 키워드<br/>
=> this.필드 : 해당 클래스에서의 필드<br/>
=> 변수명이나 메서드명이 겹칠때 등등사용...

<br/><br/>

# ◆ 분기처리
for문등에서 처리하기 힘든 분기처리를 하기 위해 사용하는 방법으로 continue키워드를 사용하여 원하는 지점으로 이동시킨다.
{% highlight ruby %}
row :
    System.out.println("분기");
    
continue row;  // row로 다시 돌아감!
{% endhighlight %}

<br/>

# ◆ 객체 비교
<font color="orange">객체.compareTo(객체)</font> <br/>
이 메소드가 반환하는 int형 정수가 양수일 때는 앞에 객체가 큰 것이고, 음수일대는 매개변수 객체가 더 큰 값을 가진 것이다.<br/>
=> 단, 객체 클래스 내부에 compareTo메서드가 오버라이드 되어있어야 한다.<br/> 
( 보통 라이브러리 API객체들 같은 경우에 대부분 해당 메서드가 오버라이드 되어있다. )<br/>
=> 스트링 객체는 맨 앞문자의 크기를 비교하고 같을 경우 그다음 문자 순으로 비교된다.





<br/>