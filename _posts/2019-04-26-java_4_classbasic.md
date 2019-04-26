---
layout: post
title: "4. 클래스(객체설계)"
tags: [ java ]
date: 2019-04-26
categories: [ java ]
---

<p align="center">
    클래스의 설계 및 메서드, 주요 키워드에 대해 알아보자.
</p><br/>

# ◆ 객체지향과 절차지향의 차이점
- 절차지향방식: 데이터 값들을 프로시저에 항상 넘겨주어야 한다.
- 객체지향방식: 데이터 값들을 넘겨줄 필요가 없다.

<br/><br/>

# ◆ 객체 연결
{% highlight ruby %}
Point p2 = p1 ;
{% endhighlight %}
p1의 값을 바꾸면 p2도 바뀌게 되고, p2를 바꾸면 p1의 값도 같이 바뀌게 된다.
<br/>
즉 p2와 p1은 같은 객체 Instance
<br/>
단, = 기호를 이용하여 다른 객체를 대입하게 되면, p1과 p2는 다른 객체가 된다.

<br/><br/>

# ◆ 객체를 제어하기 위한 변수
new Point(); 만으로도 객체 생성은 가능하다.<br/>
하지만 이렇게 생성된 객체는 제어를 할 수 없기 때문에
Point p = new Point(); 형식으로 객체를 제어할 변수가 있어야 제어가 가능하다!
<br/>
( 제어 할 필요가 없는 객체일 경우 변수를 꼭 만들 필요는 없다. )

<br/>

#### ▶ 같은 값을 가진 다른 객체가 필요할 때
{% highlight ruby%}
Rectangle r2 = new Rectangle(r1);   
{% endhighlight %}
=> r1과 같은 값을 가진 객체가 생성됨.
=> r2==r1 을 비교하면 false 
<br/>
( 서로 다른 객체이다.) 
<br/>
단, 해당 클래스에서 그러한 생성자(Constructor)가 만들어져 있는 경우에만 가능!

<br/><br/>

# ◆ toString 메서드
println으로 <font color="orange">객체 변수를 변수이름만으로 호출할 경우 자동적으로 toString()이 호출</font>된다. ( toString 메서드는 String을 반환 )
<br/>
따라서 해당 객체 클래스에 toString() 메서드가 없는 경우, 부모(상위)클래스의 toString()이 호출된다. 
( 최상위 클래스인 Object에 toString() 메서드가 있다.）
<br/>
> 따라서 <font color="orange">객체변수 이름만으로 무언가 출력하고자 할 경우 toString() 메서드를 오버라이드</font> 해야 한다.

<br/><br/>

# ◆ 객체, 클래스, 인스턴스 
  - 객체(Object) = 머릿속에 떠오르는 추상적인 상태
  - 클래스(Class) = 객체를 프로그램으로 구현 해둔 것 ( 객체의 청사진 )
  - 인스턴스(Instance) = 설계 해둔 CLASS를 토대로 실제 객체를 생성하는 것
  <br/>
  ( 프로그램 적 실체화 )
=> 하나의 Object(객체)를 표현하기 위해서 하나의 class가 필요.<br/>
완성된 class를 토대로 여러 개의 instance가 생성이 가능.
<br/>
ex) A라는 클래스 작성 후 A a = new A(), A b = new A() 와 같이 여러 개를 생성할 수 있다.

<br/><br/>

# ◆ 클래스의 구조
- 필드(field): 객체의 데이터 ( 클래스 변수 )
- 메서드(method): 객체의 기능 ( 클래스 메서드 )
- 생성자(constructor): 객체생성시의 작업

<br/><br/>

# ◆ 클래스 설계
- 클래스의 이름의 <font color="orange">첫 문자는 대문자로 시작</font>한다.
- <font color="hotpink">하나의 java파일 안에 public클래스는 하나만 만들 수 있다.</font>
- 클래스를 통해 생성된 객체 변수는 실제 객체가 아니라 해당 객체가 가지고 있는 레퍼런스값을 저장하고 있는 변수이다.<br/>
> 레퍼런스값을 가지고 있는 객체 변수에 null값을 넣으면 객체 연결이 끊김으로 가비지컬렉션이 발생하여 메모리가 해제되고, 해당 객체는 더 이상 사용할 수 없는 상태가 된다.

{% highlight ruby %}
public class Car{
	// 필드
	public String color;
	public int price;
	
	// 생성자
	public Car() {
		System.out.println("생성자 호출");
	}
	
	// 메서드
	public void isColor() {
		System.out.println("색상 : " + this.color);
	}
}
{% endhighlight %}

<br/>

# ◆ 메서드 설계
- 메서드의 이름은 <font color="orange">첫 문자 소문자로 시작</font>한다. <br/>
( 단어와 단어의 연결의 시작 단어는 대문자로 시작 )
- 메서드의 정의는 <font color="orange">‘접근자’ ‘반환형’ ‘메서드이름’(매개변수){}</font> 로 구성한다.
{% highlight ruby%}
public void getCall(int a){
	System.out.println(“이 메서드의 접근자는 public, 반환형은 void입니다.);
	System.out.println(“매개변수출력: “ + a);
} 
{% endhighlight %}

<br/><br/>

# ◆ 생성자 (Constructor)
- 생성자는 <font color="orange">인스턴스화시 호출되는 특수 메서드</font> 
<br/>
   ( 형태는 <font color="orange">반환형이 없는 class명과 이름이 같은 메서드</font> 형태 )
- 하나의 클래스 안에는 반드시 하나 이상의 생성자가 있어야 한다. 
<br/>
( 여러 개는 상관 없음 )
- <font color="orange">생성자를 만들지 않으면 인스턴스화 할 시, 자동으로 기본 생성자가 생성</font>된다. 
<br/>
   ( 단, 하나라도 생성자가 있을 시, 기본 생성자는 만들어지지 않는다. )
> 기본생성자는 매개변수가 없고 아무 기능이 없는 생성자이다.

- 매개변수가 있는 생성자의 경우 보통 필드 초기화에 사용됨.
- 하나이상의 생성자를 작성할 시, 가능한 기본 생성자는 같이 만들어 두는 것이 좋음.

<br/><br/>

# ◆ 소멸자
- 객체의 연결이 끊겨 더 이상 사용하지 않은 객체를 메모리에서 해제(GC)할 때 해당 객체의 finalize()메서드가 호출된다. 
<br/>
( finalize()는 상속받는 메서드 이기 때문에 만들지 않아도 된다. )
- System.gc() 메서드를 호출하면 가비지컬렉션의 작동을 빨리 할 수 있도록 해준다.
( 일반적으로 자주 사용하는 메서드는 아님 )

▶ 소멸자 형태
{% highlight ruby %}
@Override
protected void finalize() throws Throwable{
	super.finalize();
}
{% endhighlight %}

<br/>

# ◆ 패키지 
하나하나의 객체들을 설계해서 객체 간 관계를 의미 있게 그룹화 할 수 있게 지원하는 개념( <font color="orange">패키지는 실제로 폴더로 생성</font>된다. )<br/>

- 패키지 생성 : eclipse 상에서, 프로젝트 src우클릭 new package
> 패키지를 생성할 때 .을 찍으면 하위 폴더로 더 구성할 수 있다.<br/>
   model.human 이라는 이름으로 패키지를 생성하게 되면 model패키지(폴더) 안에 human패키지가 생성된다.
   
- 같은 패키지 안에서는 다른 클래스(객체)를 별도의 작업 없이 사용할 수 있지만,
   <font color="hotpink">다른 패키지에 있는 클래스를 사용하기 위해서는 아래 두 가지 방법으로 접근</font> 할 수 있다.
   <br/><br/>
   
  <b>방법1.</b> 사용하고자 하는 클래스를 <font color="orange">사용할 때마다 해당 클래스의 소속(패키지)을 지정</font>해준다.
  다른 패키지에 있는 클래스에서 model패키지에 있는 Unit이라는 클래스를 사용하기 위해
  앞에 소속을 붙여주고 사용한다.<br/>
  {% highlight ruby %}
  model.Unit u = new model.Unit();
  {% endhighlight %}
  ( 사용할 때 마다 소속을 붙여줘야 한다. )
  <br/>
  
  <b>방법2.</b> 1번의 방법의 번거로움을 피하기 위해 <font color="orange">import 키워드를 사용</font>한다.
  <br/>
  위와 같이 model패키지안의 Unit 클래스를 사용하기 위해 import model.Unit을 사용해주    면 같은 패키지에 있는 클래스처럼 소속을 지정해주지 않고 클래스 이름만으로 접근이 가능하다.
  <br/>
  {% highlight ruby %}
  import model.Unit;
  Unit a = new Unit();
  {% endhighlight %}
       
> import할 때에 모든을 의미하는 \*을 사용하면 특정 패키지 안의 모든 클래스들을 import할 수도 있다. 
Ex) import model.\*
  
▶ import 시 주의<br/> 
각각 다른 패키지에 있는 같은 이름을 가진 클래스를 import 시킬 수 없다.
{% highlight ruby %}
import java.awt.List;  
import java.util.List;  => 불가능
{% endhighlight %}
=> 한 쪽은 소속 명을 계속 써 줘야할 상황도 있다.

<br/><br/>

# ◆ 캡슐화( Encapsulation )
캡슐화란 관련된 기능이나 데이터를 한 곳으로 모아서 설계 하는 것<br/>
OR 꼭 필요한 데이터나 기능만 외부로 노출 ( <font color="hotpink">정보은닉(Information Hiding )</font> )하는 것으로 객체지향에 있어 중요한 개념이다.

<br/><br/>

# ◆ 접근 제한자
클래스를 포함하여 클래스를 구성하는 필드, 메서드, 생성자에서 사용할 수 있는 접근 허용 범위에 사용되는 키워드(시야) / 데이터 은닉에 사용된다.<br/>

#### ▶ 필드, 메서드, 생성자에 적용할 수 있는 접근 제한자
  - <b>private[-]</b> : 해당 <font color="orange">클래스 내부에서만 접근</font> 가능.
  - <b>public[+]</b> : 타 패키지 <font color="orange">어디에서도 접근이 가능</font>.
  - <b>protected[#]</b> : 타 패키지에 설계된 <font color="orange">특수 관계(상속)의 객체에서 접근</font>이 가능
  - <b>(package)[ ]</b> : <font color="orange">같은 패키지 내에서만</font> 접근 가능. ( default )
  <br/>
  [ ] 안의 부호는 클래스 UML (Unified Modeling Language )에서 시야를 표기할 때 쓰는 기호 <br/>
  \* UML: 개발자들 간에 사용되는 일종의 표 ( 다른 언어에서는 다른 키워드로 구현이 될     수 있기 때문에 사용되는 통합 부호)
  <br/>
  > package는 직접 지정할 수 없고 쓰지 않았을 때만 적용되는 접근제한자이다.
  <br/>
  따라서, package 클래스는 다른 패키지에서 import또한 할 수 없는 클래스!<br/><br/>
  \* (package)클래스에서 public메서드를 사용하는 것은 어차피 다른 패키지에서 접근할 수 없는 클래스이기 때문에 무의미하다.<br/>
  \* (package)클래스는 왼쪽 자바 파일에 ▲모양의 표시가 뜬다.<br/>
  
- 클래스에 적용 시킬 수 있는 접근 제한자는 (package)와 public 밖에 없다.
- 일반적으로 멤버 변수는 외부 접근을 제한(private), 멤버메서드는 허용(public)한다.
- (package)클래스일 경우 하나의 자바 파일에 여러 개의 클래스를 만들 수 있다.
하지만, public클래스를 사용할 때에는 자바 파일의 이름과 클래스명이 일치해야 한다.<br/>
(즉, 하나의 자바파일 안에 public클래스는 하나이하만 존재해야 하고, (package)클래스는 여러 개가 존재해도 상관은 없다. 하지만 public클래스가 있을 경우 자바의 파일명과 일치 해야하고 main메서드도 public클래스 내부에 있어야 한다.)
- 객체지향 5 원칙인 SOLID의 O에 해당하는 내용. ( 개방 과 패쇠 )

<br/><br/>

# ◆ 접근제한자에 따른 에러 메시지  
#### ▶ 사용하고자 하는 메서드가 해당 클래스에 있지 않은 경우.
   The method convertToAr(null, null) is undefined for the type Date
   => Undefined
#### ▶ 해당 메서드가 있지만 private으로 접근할 수 없는 경우
   The method convertToAbbr(StringBuilder, String) from the type Date is not         visible
   => Not Visible

<br/><br/>

# ◆ static키워드 
instance마다 할당되는 것이 아니라, 클래스이름으로 하나만 할당되게 할 변수 또는 메서드, static키워드를 붙인 필드나 메서드는 <font color="orange">클래스의 이름만으로 접근이 가능</font>하고, <font color="orange">인스턴스간 공유</font>되는 것이다.
- field나 method 에 붙일 수 있음
- 필드에 붙이는 경우는 개별적인 유지가 필요 할 때
- 메서드에 붙이는 경우는 static필드를 제어할 때<br/>
( static field를 꼭 static method에서 제어해야 하는 것은 아니나,
클래스이름으로 접근할 수 있도록 작동되기 위해 <font color="orange">static field는 static method에서 제어하는 것이 가독성이 높아진다!</font>)
- static method에서는 일반 instance field나 instance method를 사용하는 것은 불가능하다

<br/><br/>

# ◆ static구문 
클래스 안에 <font color="orange">static {  }</font> 이라는 구문 중괄호 안에 작업을 해놓으면, 해당클래스의 <font color="orange">최초 객체 생성 시에만 작업</font>이 일어난다.( 두 번째 객체생성부터는 static{} 은 호출되지 않음 )
{% highlight ruby %}
class A{ 
    static{ 
        System.out.println(“a”); 
    } 
}
{% endhighlight %}
A클래스의 최초 객체 생성 시에만 static구문의 작업이 일어난다. (“a”호출 한번만 )

<br/><br/>

# ◆ 메서드로만 이루어진 클래스 
필드 없이 메서드로만 구성되어있는 클래스의 경우 클래스이름으로 메서드만 사용하기 때문에 static메서드로 만들어진다.
<br/>
또한 이 경우 객체 생성이 필요 없기 때문에 private 생성자로 객체 생성을 막아 둔다.
<br/>
( private 작업 없이 생성자를 만들지 않을 경우, 기본 생성자가 자동으로 생성되기 때문 )
<br/>
ex) Math 객체

<br/><br/>

# ◆ this 키워드
this는 지금 <font color="hotpink">현재 클래스 객체를 의미</font> this.필드는 현재 클래스의 멤버 변수를 의미하며, this() 는 현재클래스의 기본생성자호출<br/><br/>

▶매개변수의 변수명과 현재 클래스의 필드의 변수명이 같을 경우 this키워드를 사용하여 구분할 수 있다.
{% highlight ruby %}
public A(int a, int b){
    this.a = a;
    this.b = b;
}
{% endhighlight %}

▶ 생성자 안에서 생성자를 호출할 수 있다.
<br/>
ex) 인자 없는 생성자 안에서 this(int a)를 호출할 경우 매개변수 하나를 받는 생성자를 호출한다. ( 인자 있는 생성자가 만들어져 있을 경우에만..)
<br/>

#### cf ) super 키워드
부모클래스를 의미하는 키워드로, super()는 부모클래스의 생성자 호출을 의미한다.<br/>
즉, super는 부모클래스의 this와 같다.




<br/>