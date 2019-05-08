---
layout: post
title: "16. 멀티쓰레드(다중작업)"
tags: [ java, multithread ]
date: 2019-05-08
categories: [ java ]
---

<p align="center">
    자바의 흐름은 main메서드를 통해 진행된다. 하지만 상황에 따라 main의 흐름 하나만으로는 처리하기 어려운 작업들이 있기 때문에 쓰레드라는 개념의 다중 작업을 지원해준다.
</p><br/>

# ◆ 쓰레드( Thread )
메인흐름 하나만 사용해서는 구현이 불가능한 프로그램들이 존재한다.<br/> 
TCP에서 다중접속자를 처리한다거나, 백 그라운드 작업을 구현 할 때는 메인 외의
보조 Thread를 이용해서 여러 개의 쓰레드를 구현 할 수 있다.
( main도 하나의 쓰레드 개념이다. )
-  Single Thread 
:  메인 쓰레드 하나만 사용하는 프로그램
-  Multi Thread 
:  메인 외에 추가적으로 여러 쓰레드를 동시에 사용하는 프로그램

<br/>

# ◆ 쓰레드 설계 방법
쓰레드를 설계하는 방법으로는 크게 Thread클래스를 상속받는 <font color="orange">extends Thread</font>방법과, Runnable인터페이스를 구현하는 <font color="orange">implements Runnable</font>방법 두 가지가 있다.

<br/>

#### ▶ extends Thread를 이용한 쓰레드 설계
1. <font color="orange">Thread클래스를 상속</font>받는 클래스를 생성하여, <font color="orange">run()메서드를 Override</font>한다.
{% highlight ruby %}
class Alpha extends Thread { // Thread상속
    @Override // run()메서드 오버라이드
    public void run() {
        for (int cnt = 1; cnt <= 20; cnt++) {
            System.out.println("Alpha work");
        }
    }
}
{% endhighlight %}

<br/>

2. 메인에서 설계해 놓은 extends Thread한 객체를 생성하여 <font color="orange">start()메서드로 쓰레드를 실행</font>시킨다.
{% highlight ruby %}
main{ 
Alpha a = new Alpha(); 
a.start();
}
{% endhighlight %}

<br/>

#### ▶ implements Runnable을 이용한 쓰레드 설계
1. <font color="orange">Runnable인터페이스를 구현</font>하여 <font color="orange">run()메서드를 Override</font>하여 쓰레드를 설계한다.
{% highlight ruby %}
class Beta implements Runnable {
    @Override
    public void run() {
        for (int cnt = 1; cnt <= 20; cnt++) {
            System.out.println("Beta work");
        }
    }
}
{% endhighlight %}

<br/>

2. 메인에서 <font color="orange">설계해둔 쓰레드구현 객체를 인자로 하는 Thread객체를 생성</font>하여 해당 Thread객체의 <font color="orange">start()메서드로 쓰레드를 실행</font>한다.
{% highlight ruby %}
main{
    Beta b = new Beta();
    Thread sub = new Thread(b);
    sub.start();
}
{% endhighlight %}

<br/>

- 쓰레드는 하나의 객체(인스턴스)당 start()메서드를 한 번만 호출 할 수 있기 때문에, <font color="orange">여러개의 쓰레드를 실행하고자 하는 경우 각각 객체생성을 따로 해 주어야 한다.</font>
- run()메서드를 Override할 클래스를 작성할 시, 생성자의 인자로 데이터를 보내면 메인에서 입력한 데이터를 보낼 수 있다.( 따라서 쓰레드에서 다른 객체 제어 가능 )

<br/><br/>

# ◆ 쓰레드 제어
쓰레드를 생성해서 start()를 걸게 되면, 작동 되어지는 쓰레드의 작업이 종료되면 자동적으로 종료되지만, 필요하다면 수동으로 제어를 해 줄 수도 있다! ( 작동시킨 곳에서 )
<br/>

#### ▶ Thread.activeCount()
현재 활성 되어있는 쓰레드의 개수반환<br/> 
( main메서드기본 1개 포함, 다이얼로그객체도 쓰레드에 포함 될 수 있다. )

<br/>

#### ▶ 쓰레드 활성화 객체.interrupt();
활성화중인 쓰레드객체에 interrupt를 발생시킨다.<br/>
=> 해당 클래스의 run() 메서드 안에서 <font color="orange">this.isInterrupted();</font>로 boolean확인할 수 있다.<br/>
이 메서드를 사용하여, <font color="orange">break등을 통해 메서드를 중지</font>시킨다거나 하는 제어를 할 수 있다.<br/>

<br/>

#### ▶ 쓰레드 활성화 객체.join()
join()메서드는 <font color="orange">쓰레드의 작업이 끝날 때 까지 main메서드에서 작동을 멈추고 기다리는 메서드</font>이다.<br/>
( 쓰레드의 작업이 끝난 후 데이터를 이용하거나, 끝난 후 다른 작업이 필요할 경우 쓰인다 )

> join(1000); 등을 이용해 main이 기다려 주는 시간을 설정 할 수도 있다.
( 단 join메서드는 동기화처리가 되어있지 않은 클래스들은 무의미하다. )

<br/>

# ◆ 동기화(synchronized)
여러 쓰레드에서 하나의 자원(객체)을 접근해서 사용되게 될 때 고려해야 되는 문제이다.<br/>
여러 활성화된 쓰레드에서 하나의 객체메서드를 접근 할 경우, 메서드호출이 씹힌다거나, 접근할 때의 데이터들이 달라서 원하고자 하는 <font color="orange">데이터의 안정성을 보장</font> 받을 수 없다.<br/>
따라서 이런 단점들을 보완해주기 위해 동기화(synchronized)가 필요하다.

<br/>
#### ▶ 동기화 특징
동기화(synchronized) 처리를 하게 되면, <font color="orange">해당 메서드나 객체에 동시에 접근이 불가능</font>하기 때문에 데이터의 안정성을 보장 받을 수 있다.
> Vector 클래스의 경우 동기화(synchronized)처리가 되어있는 메서드이기 때문에, 멀티 쓰레드 작업 시 데이터들이 꼬이지 않지만,<br/> 
ArrayList등의 클래스의 경우 동기화(synchronized)처리가 되어있지 않기 때문에 데이터의 안정성을 보장 받을 수 없다.

<br/>

#### ▶ 동기화 처리방법
1. 메서드 동기화 처리
: 메서드 반환형 앞에 synchronized키워드를 붙이면 해당 메서드에 동시접근 불가능
{% highlight ruby %}
public synchronized void withdraw(int m){
    ... 
}
{% endhighlight %}
2. 객체 동기화 처리
: run()메서드 안에서 synchronized(객체)를 하게 되면 해당 객체에 동시접근이 불가능 <br/>
( 객체 lock )
{% highlight ruby %}
@Override
public void run() {
    synchronized(객체) {
        객체제어
    }
}
{% endhighlight %}









<br/>