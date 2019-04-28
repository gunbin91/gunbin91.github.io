---
layout: post
title: "7. 인터페이스 및 특수설계"
tags: [ java, interface, enum, anotation ]
date: 2019-04-28
categories: [ java ]
---

<p align="center">
    추상클래스와 비슷한 인터페이스란것과 자주 쓰이지는 않지만 클래스와 비슷한 구조를 가진 객체를 알아보자.
</p><br/>

# ◆ Interface ( 인터페이스 )
일반 클래스와 다르게 <font color="hotpink">static final field(변수)와 abstract method(메서드)만을 가질 수 있고</font>, <font color="hotpink">객체 생성이 불가능</font>한 형태의 추상클래스와 비슷한 구조. (일반 변수와, 메서드를 가질 수 없다)

{% highlight ruby %}
// class가 아닌 interface를 이용하여 작성한다
public interface CPU{ 
    static final int MAX = 1;
    abstract void sum();  
    // 인터페이스에서는 abstract를 안 붙여도 붙인 것으로 인식하고,
    추상메서드처럼 중괄호({})를 쓰지 않고 세미콜론으로 끝낸다.
}
{% endhighlight %}
- 인터페이스를 사용하기 위해서 상속의 개념과 비슷한 <font color="orange">implements(구현)을 해야 한다</font>.<br/>
클래스 뒤에 extends와 비슷하게 implements 인터페이스클래스로 구현한다.<br/>

> 인터페이스 또한 캐스팅이 가능하기 때문에 인터페이스 선언 변수 안에 구현클래스객체 생성으로 캐스팅이 가능하다.<br/>
( 인터페이스를 사용하는 가장 큰 이유 중 하나가 다양한 클래스타입을 가질 수 있기 때문이다. )

- 인터페이스는 상속과 다르게 <font color="hotpink">여러 개를 구현할 수 있다</font>. (다형성)
- implements한 인터페이스에 있는 <font color="orange">모든 메서드는 반드시 오버라이드 해야한다</font>.
- 클래스 설계 시 인터페이스를 거치는 것이 좋다 (추후 수정 할 때 수정 범위가 줄어든다.)<br/>
<b>light-coupling:</b> 상위 객체 변수에 하위 객체를 생성 하는 것.<br/>
<b>tight-coupling:</b> 같은 객체 변수에 같은 객체를 생성 하는 것.<br/>
- 인터페이스의 메서드는 <font color="orange">public abstract 밖에 없기 때문에 이 키워드를 생략해도 자동으로 있는 것으로 인식</font>한다.
- JDK1.8버전부터는 default키워드를 이용하여 인터페이스에서도 메서드 구현이 가능하다.(defalut되어 있는 메서드는 자동 완성할 때 D표기가 돼있음)
{% highlight ruby %}
public defalut boolean bol(int a){ return true; }
{% endhighlight %}
- 인터페이스는 인터페이스를 extends 할 수 있다.
- 일반 클래스는 여러 개의 인터페이스를 동시에 구현(implements)할 수 있다.

<br/><br/>

# ◆ Enum
미리 정해진 데이터를 설정해 두고 사용하는 열거형 객체로, 객체 생성은 불가능하다.
#### ▶enum클래스 정의
{% highlight ruby %}
    public enum Direction{
       UP(1,2), DOWN(2,3), RIGHT(3,3),LEFT(4,4);
       int a,b;
       Direction( int a, int b){  this.a=a;  this.b=b;  }  
       // 접근 제한자를 설정할 수 없음.
    }
{% endhighlight %}

#### ▶main에서 사용 :
{% highlight ruby %}
Direction d = Direction.UP;
System.out.println(Direction.DOWN);
System.out.println(d.LEFT.a);
{% endhighlight %}

#### ▶ switch 문에서 처리 가능한 데이터 타입
: 정수, String, enum데이터
{% highlight ruby %}
switch(d){
case RIGHT :
case LEFT :
}
//if문에서 사용
if( d == Direction.LEFT){}
{% endhighlight %}
클래스 선언과 동시에 미리 객체를 생성시켜 놓는 것과 비슷하게 생각하면 됨

# ◆ Enum객체 예시
{% highlight ruby %}
public enum Planet {
    VENUS(6.052e3,4867e24,1), EARTH(6.371e3,5.972e24,2), MARS(3.390e3, 6.4171e23,3);
    
    final double mass;
    final double radius;
    int a;
    int b=55;
    
    Planet(double radius, double mass, int a){
        this.mass = mass;
        this.radius = radius;
        this.a = a;
    }
    
    public void pt() {
        System.out.println
        ("enum_Print----" + mass + " : " + radius + " : " + a + " : " + b);
    }
}
{% endhighlight%}

#### ▶ Enum데이터와 비슷한 구조를 가진 클래스 만들기
{% highlight ruby %}
public class Car {
    public static final Car BENZ;
    public static final Car BMW;
    
    static {
        BENZ = new Car(300, "벤츠");
        BMW = new Car(290, "비엠더블유");
    }
    
    final int speed;
    final String name;
    
    private Car(int speed, String name) {
        this.speed = speed;
        this.name = name;
    }
}
{% endhighlight %}
차이점 : Enum이 아닌 클래스로 만든 Car객체의 경우 switch문 등에서 객체 값을 넣을 수 없음.

<br/><br/>

# ◆ annotation ( 원뜻은 주석 )
프로그램에 직접적인 영향은 없지만 컴파일러 혹은 타 시스템에 정보를 제공하는 역할을 함.<br/>
(기계가 인식하는 주석) @Override 등등...<br/>
=> 우 클릭 new -> annotation 을 하면 public @interface 형식이 만들어짐<br/>

{% highlight ruby %} 
public @interface Comment {
    String writer();
    String date();
    String about();
    int version() default 1;
}

@Comment(writer="yoon", date="2017-11-07", about="use annotation")
public class AA{}
{% endhighlight %}
=> version은 default값이 있기 때문에 설정하지 않아도 가능하나,
나머지 것들은 default값이 설정되어 있지 않기 때문에 꼭 써 줘야하는 부분이다.<br/>

## ◆ Annotation활용
#### ▶ @Override 
오버라이드를 구현 할 때 위에 적어두면 오버라이드 메서드를 구분할 수 있고 오버라이드가 된 건지 확인이 가능하다.

#### ▶ @Deprecated  
구현한 클래스에서 더 이상 필요가 없을 것 같을 때 언젠가 지워질 메서드라고 메서드를 사용하는 이용자에게 줄을 그어 알려줌.

#### ▶ /** 로 시작하는 주석을 달면 javadoc의 정보에서 자신이 작성한 정보를 볼 수 있음.
우클릭 -> Export -> javadoc => (jdk->bin->javadoc)추가 <br/>
=> doc파일이 만들어지고 해당 클래스의 정보를 볼 수 있다.

#### ▶  @SuppressWarnings({"deprecation", "null", unused})
deprecation, null, unused( 적어놓은 어노테이션 )에 대한 경고 메시지를 제거.




<br/>