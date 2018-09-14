---
layout: post
title: "7. 클래스"
tags: [ python, python class, 파이썬 ]
date: 2018-09-12
categories: [ python ]
---

<p align="center">
  파이썬 또한 객체지향 언어이기 때문에 클래스가 있다.  
</p><br/>

# 클래스( Class )
객체지향 프로그래밍을 위해 설계하는 자바의 클래스와 같은 개념
<br/>

# 클래스 설계
클래스를 설계할 때는 <font color="orange">'class 클래스명 : '</font>을 통해 작성한다.
{% highlight ruby %}
class Person : 
    pass
{% endhighlight %}
<br/><br/>

# 객체 생성
위와 같이 클래스를 작성했을 경우
{% highlight ruby %}
p = Person()
{% endhighlight %}
&nbsp;<font color="orange">'클래스명()'으로 객체를 생성</font>할 수가 있다.
<br/><br/>

# 클래스 메서드 
클래스에서 메서드를 정의할 때 일반적인 함수의 정의와 똑같지만,<br/>
파이썬에서는 클래스 메서드를 정의할 때 <font color="deeppink">첫번째 매개 인자로 'self'를 받아야 한다</font>는 점이 다르다.<br/>
{% highlight ruby %}
class Person : 
    
    def sum(self, a, b) :
        pass
{% endhighlight %}
> self는 자바의 this와 비슷한 개념으로 객체를 생성했을 때 해당 객체를 넘겨받는 역할을 하며,<br/> self라는 이름으로 쓰지 않아도 작동은 되지만 self로 쓰는 것이 원칙이다.<br/>
또한, 클래스메서드를 호출할 때 파이썬은 알아서 self값을 넘겨주기 때문에 <font color="deeppink">클래스 함수 호출 시 self에 해당하는 값을 넘겨줄 필요는 없다.</font>
<br/><br/>

# init메서드
파이썬의 클래스에는 여러가지 특별한 메서드 이름이 존재하는데
그 중에서 <font color="deeppink">init메서드는 해당 클래스를 인스턴스화(객체생성)할 때 호출</font>된다. ( 자바의 생성자 역할 )<br/>

- <font color="deeppink">init메서드 정의</font><br/>
init메서드를 정의할 때는 양쪽에 언더바 두 개를 이용하여 정의하도록 한다.<br/>
{% highlight ruby %}
def __init__(self, name) :
	self.name = name
{% endhighlight %}
<br/>

- <font color="deeppink">객체 생성시</font><br/>
p = Person("gunbin") 처럼 <font color="orange">self를 제외한 init메서드의 인자</font>를 넘겨주어야 한다.<br/>
이는 다른 함수 호출 시에도 똑같이 적용된다.
<br/><br/>

# 클래스 변수와 객체 변수
파이썬에서 클래스의 변수는 클래스 변수와 객체 변수로 나누어져 있는데,<br/> <font color="deeppink">클래스 변수</font>는 자바의 static변수와 같이 <font color="deeppink">모든 객체들이 공유하는 변수</font>이며, <font color="orange">객체 변수</font>는 해당 <font color="orange">객체만이 사용할 수 있는 변수</font>이다.<br/> 
( 단, 클래스 변수와 객체 변수의 이름이 같을 경우 객체 변수가 우선시 된다. )<br/>

- <font color="deeppink">클래스 변수</font><br/>
클래스 변수는 클래스를 정의할 때 <font color="orange">메서드 바깥쪽으로 정의</font>하면 클래스변수가 된다.<br/>
이를 제어하고자 할 때는 <font color="orange">'클래스명.클래스변수'</font> 또는 'self.class.클래스변수'를 통하여 제어가 가능하다.
<br/><br/>

- <font color="deeppink">객체 변수</font><br/>
객체 변수는 일반적으로 클래스 <font color="orange">메서드 안에서 정의 된 필드</font>들이다.<br/>
&nbsp;<font color="orange">객체변수를 제어하기 위해서는 꼭 slef를 앞에 붙여서 사용</font>해야 한다.

<br/>
{% highlight ruby %}
class person :
    a = 10 # 클래스변수
    def deb(self, i) :
        self.b = i # 객체변수

one = person()
one.deb(5)

print(person.a)
print(one.b)

실행결과
=> 10
5
{% endhighlight %}
> 자바의 구조와 많이 다르기 때문에 주의해서 사용하도록 하자.

# @classmethod
@는 데코레이터라고 부르며, 메서드 위에 선언해 두어 해당 메서드의 기능을 지정해 줄 수도 있다.<br/>
&nbsp;<font color="deeppink">@classmethod는 클래스 변수를 제어하는 클래스메서드를 정의</font>할 때 쓰는 데코레이터 이며, 해당 메서드를 정의할 때는 self와 마찬가지로 <font color="orange">'cls'라는 클래스를 지칭하는 변수를 인자로 받아야 한다.</font><br/>
마찬가지로 <font color="orange">클래스변수를 제어하기 위해서는 cls를 변수앞에 붙여서 제어</font>해야 한다.
{% highlight ruby %}
class person :
    a = 10 # 클래스변수

    @classmethod
    def deb(cls, i) :
        cls.a = i

person.deb(5)
print(person.a)

실행결과
=> 5
{% endhighlight %}
<br/>

# 상속
기본 클래스의 멤버를 서브클래스가 상속받아 사용할 수 있다.
<br/><br/>

#### ▶ 상속받기
클래스를 정의할 때 인자를 받지 않지만, 상속받는 클래스를 정의할 경우 <font color="orange">클래스의 인자로 상속받을 기본클래스명을 입력</font>한다.<br/>
ex ) SchoolMember를 상속받는 Student클래스 정의
{% highlight ruby %}
class Student(SchoolMember) : 
    pass
{% endhighlight %}
<br/>

#### ▶ 서브클래스의 init메서드 정의
서브 클래스 객체의 init메서드가 호출 될 때 기본 클래스의 init메서드가 같이 호출되는 것이 아니기 때문에 <font color="deeppink">서브클래스의 init메서드에서 기본클래스의 init메서드가 필요할 경우 명시적으로 호출할 필요가 있다.</font>
{% highlight ruby %}
def __init__(self,name,age, salary) :
	SchoolMember.__init__(self,name,age)
	self.salary = salary
{% endhighlight %}

> 기본적으로 클래스 함수를 호출 할 때 self를 인자로 보낼 필요가 없지만, <font color="deeppink">서브 클래스의 메서드정의에서 기본 클래스의 메서드의 호출이 필요한 경우 self를 인자로 보내주어야 한다.</font>

# 그외 파이썬 클래스 특징

- 오버라이딩 가능

- 클래스에도 DocString속성이 있다. 클래스명.doc 또는 클래스명.메서드명.doc

- 언더바 두개로 쌓여져 있는 멤버들은 자바의 private와 같이 외부로 공개되는 것을 막는 역할을 한다.<br/>
( 기본적으로 파이썬의 모든 멤버는 자바의 public형 )
{% highlight ruby %}
class Person :
    # public
    a = 5
    # private
    __b__ = 10
{% endhighlight %}

<br/>