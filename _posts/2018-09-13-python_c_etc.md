---
layout: post
title: "12. 그외 파이썬 특징"
tags: [ python, python api ]
date: 2018-09-13
categories: [ python ]
---

<p align="center">
    파이썬만의 특별한 문법들에 대해 알아보자.
</p><br/>

# 두 개 이상의 결과값 반환
파이썬에서는 두 개 이상의 값을 반환할 수가 있다.<br/>
단일 데이터가 아닌, <font color="orange">튜플을 반환할 경우 해당 튜플의 데이터 수 만큼 반환</font>이 가능해지고, 이를 동시에 변수에 대입할 수 있다. 
즉, <font color="orange">튜플은 해당 데이터 수만큼 동시에 변수에 대입이 가능</font>하다.
{% highlight ruby %}
def get_sn() :
	return (2,"ss")
    
a,b = get_sn()
print(a)
print(b)
{% endhighlight %}
<br/>

- 앞서 튜플에 대한 설명에서 <font color="orange">튜플은 괄호 없이 선언이 가능</font>하다는 것을 알고있다.<br/>
따라서 아래와 같은 코드가 가능해지며, <font color="orange">함수의 리턴또한 괄호 없이 여러개를 반환</font>할 수 있다.
{% highlight ruby %}
a = 1, 2, 3
print(a)

=> (1, 2, 3)
{% endhighlight %}
<br/><br/>

# 특별한 메서드들
- <font color="orange">_ _ init _ _(self, …)</font><br/>
자바에서 생성자와 같이 파이썬에서도 객체가 생성될 때 해당 객체클래스에 정의되어 있는 init메서드를 호출 시킨다.
<br/><br/>

- <font color="orange">_ _del_ _(self)</font><br/>
자바의 소멸자와 같은 기능을 하는 이 메소드는 객체가 메모리에서 제거되기 직전에 호출된다.<br/>
( 그러나 언제 호출될 지 분명하지 않으므로 가능하면 사용을 피하는 것이 좋다. )<br/>
<br/><br/>

- <font color="orange">str(self)</font><br/>
print 문이라던가 str()등이 사용될 경우 호출 된다.
<br/><br/>

- <font color="orange">lt(self, other)</font><br/>
미만 연산자(<)와 동일한 역할을 하는 함수이다. 이와 비슷하게, 모든 연산자(+, -, 등등)에 해당
하는 특별한 메소드들이 하나씩 따로 존재한다.
<br/><br/>

- <font color="orange">getitem(self, key)</font><br/>
x[key]형태의 인덱싱 연산과 같은 기능을 하는 함수이다.
<br/><br/>

- <font color="orange">len(self)</font><br/>
열거형 객체의 길이를 얻어 오기 위한 내장 함수.
<br/><br/>

# 한 줄 짜리 블록
파이썬에서는 명령문의 블록을 들여쓰기로 구분하여 쓴다.<br/>
하지만, 한 블록의 명령문이 하나만 있을 경우 한 줄만 써도 가능하다. (권장사항은 아님)
{% highlight ruby %}
 if flag : print("yes")
{% endhighlight %}
<br/><br/>

# 리스트 축약
기존의 리스트를 기반으로 새로운 리스트를 생성할 때, 코드를 축약하여 리스트를 생성하는 방법
{% highlight ruby %}
listone = [2, 3, 4]
listtwo = [2*i for i in listone if i > 2]
print (listtwo)

실행결과
=> [6, 8]
{% endhighlight %}
- list를 선언하는 대괄호 안에서 for문을 작성하여 해당 반환되는 값을 list의 목록으로 생성
<br/><br/>

# 함수 인자를 튜플 또는 사전 형태로 넘겨받기
함수의 인자로 튜플 또는 사전 객체자체를 받는것이 아닌, <font color="deeppink">여러개의 인자를 보낼 때 함수내에서 자동적으로 튜플 또는 사전의 형태로 변환</font>하여 사용하도록 매개인자를 받을 수 있다.
<br/>
- 함수의 인자를 <font color="orange">튜플로 받기 위해서는 함수 정의 시 매개변수 앞에 *</font>를 써 주어야 하고, <font color="orange">사전 형태로 받기 위해서는 **</font>을 써 주어야 한다.<br/>
{% highlight ruby %}
def sum(*a) :
    sum=0
    for i in a:
        print(i)

z = (1,2,3,4,5)
sum(z) # 튜플을 튜플로 받음 => ( (1,2,3,4,5) )
sum(1,2,3,4,5) # 여러개의 인자를 하나의 튜플로 받음 => (1,2,3,4,5)

실행결과=>
(1, 2, 3, 4, 5)
1
2
3
4
5
{% endhighlight %}
> 사전 또는 튜플객체 자체를 넘겨 줄 때는 매개인자로 그냥 변수명만 써 주어도 된다.

<br/><br/>

# assert문
assert문은 어떤 조건이 참인지 아닌지 확실하게 알고 싶을 때 사용된다.<br/>
assert문을 통해 조건 확인 시 참이 아닐 경우 AssertionError이 발생된다.<br/>
ex ) mylist의 길이가 0일 경우 <br/>
assert len(mylist) >= 1 은 AssertionError 발생


# lambda
람다는 함수를 생성할 때 쓰는 예약어로, def보다 간결하게 사용할 수 있고 def가 쓰일 수 없는 곳에서도 쓸 수 있다는 장점이 있다.<br/>
lambda의 사용법은 <font color="orange">함수명 = lambda 매개변수 : 기능"</font>으로 정의가 가능하다<br/>
{% highlight ruby %}
sum = lambda a,b : a+b
sum(1,2)
{% endhighlight %}
<br/><br/>

#### ▶ lambda로 리스트에 함수 만들기
{% highlight ruby %}
myList = [ lambda a,b : a+b, lambda a,b : a*b ]

print(myList[0](2,5))
print(myList[1](2,5))

실행결과 =>
7
10
{% endhighlight %}
위와 같이 lambda로 list를 정의했을 경우, myList[0]인덱스에는 덧셈 함수가 정의되고, myList[1]인덱스에는 곱셈 함수가 정의된다.<br/>
즉, 리스트의 각각의 <font color="orange">인덱스를 함수의 이름으로 정의</font>하는것과 같다.

<br/><br/>

# f 문자열 포맷팅
파이썬 3.6버전 이상부터 사용할 수 있는 문자열 포맷팅 문법

- 변수가 미리 선언되어 있을 경우 변수명으로 바로 사용가능
{% highlight ruby %}
name = "jo"
age=12

print( f"나의 이름은{ name } 입니다. 나이는 { age+1 }입니다.")
{% endhighlight %}
<br/><br/>

# copy 모듈
객체를 직접적으로 대입하지 않고, 복사본을 만들어주는 함수
{% highlight ruby %}
from copy import copy
b = copy(a)
{% endhighlight %}
<br/><br/>

# range 함수
range함수는 list를 직접 생성하지 않고, for문등에서 간편하게 반복작업 할 수 있도록 list형태의 반복구조를 만들어주는 함수이다.

{% highlight ruby %}
for i in range(0,5) :
    print(i)
    
실행결과=>
1
2
3
4
{% endhighlight %}
- range(10)은 0~9까지의 반복구조를 만들어내며, range(3,8)은 3~7까지의 반복구조를 만들어낸다.



<br/>