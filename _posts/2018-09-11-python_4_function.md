---
layout: post
title: "4. 함수"
tags: [ python, python function, python def ]
date: 2018-09-11
categories: [ python ]
---

<p align="center">
    파이썬에서의 함수를 정의하는 방법과 특징을 알아보자.
</p><br/>

# 함수정의
파이썬에서 함수를 정의할때는 앞에 <font color="orange">'def'</font>라는 키워드를 사용하여 함수라는것을 알리고,<br/>
함수의 이름과 <font color="orange">매개변수를 타입없이 지정</font>해준다.
> def 함수명(매개변수 ...) :

{% highlight ruby %}
def sum(a, b):
    return a+b
    
print(sum(2,3))
=> 5
{% endhighlight %}

# global변수
기본적으로 함수 외부의 <font color="deeppink">전역 변수는 함수 내부에서 불러올 순 있지만 수정이 불가능</font>하다.<br/>
전역변수를 함수 내부에서 제어하기 위해서는 해당 변수가 전역변수라는 것을 선언해 주어야 하는데,<br/>
이때 사용하는 것이 'global'키워드이다. <font color="deeppink">global키워드를 전역 변수명앞에 써주면 해당 전역변수 수정이 가능</font>해 진다.<br/>

{% highlight ruby %}
x= 10
def A():
    x=5

def B():
    global x
    x=5

A()
print("A() after x",x)
B()
print("B() after x ",x)

=> 
A() after x 10
B() after x  5
{% endhighlight %}

# 함수 매개 인자 디폴트 값 설정
함수 호출 시, <font color="deeppink">정의된 함수의 매개인자 수에 맞게 매개인자를 넘겨주지 않으면 에러가 발생</font>한다.<br/>
단, <font color="deeppink">디폴트값을 미리 지정해 놓은 인자에 대해서는 꼭 넘겨줄 필요는 없게 된다.</font>
{% highlight ruby %}
def say(message, times=1) :
    print(str(times)+"."+message)

say("hi")
=> 1.hi
{% endhighlight %}

> 주의) 함수 정의시 디폴트값이 정의되어 있는 매개인자의 경우 제일 뒤쪽에 배치되어야 한다.<br/> 
Ex ) def say(message, times=1, a)는 불가!

# 키워드 인수
함수 호출 시 꼭 정의된 매개인자의 순서에 따라 매개인자를 넘겨주는 것이 아닌, <font color="deeppink">정의된 매개인자의 변수명을 통하여 순서에 상관없이 넘겨 주는것이 가능</font>하다.
{% highlight ruby %}
def func(a, b, c) :
 	print('a is', a, 'and b is', b, 'and c is', c)

func(c=100,b=50,a=5)
=> a is 5 and b is 50 and c is 100
{% endhighlight %}

# pass키워드
아무 기능을 하지 않고 넘어갈 때 사용한다.<br/>
내용이 비어있을 경우 에러를 발생 시킬 수 있기 때문에 <font color="deeppink">pass</font>라는 키워드를 넣어 <font color="deeppink">아무 기능없는 구간</font>을 만들기도 한다.<br/>
또한 파이썬에는 <font color="deeppink">None</font>이라는 데이터도 있는데, 자바의 null과 비슷하게 쓰인다.

# DocString 속성
함수의 주석 ( 설명 스트링 )<br/>
DocString은 일반적으로 첫째 줄의 첫 문자는 대문자, 마지막 문자는 마침표로 끝낸다.<br/>
두번째 줄은 비워두고 세번째 줄부터 설명<br/>

- DocString 반환
<br/> <font color="orange">'함수명._ _doc_ _'</font> 을 호출하면 해당 함수의 DocString을 str형으로 반환해준다.<br/>
{% highlight ruby %}
print_max.__doc__
{% endhighlight %}

<br/>
