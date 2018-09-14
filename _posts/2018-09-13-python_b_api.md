---
layout: post
title: "11. 파이썬 내장함수"
tags: [ python, python api, 파이썬 ]
date: 2018-09-13
categories: [ python ]
---

<p align="center">
    파이썬에 기본적으로 내장되어있는 유용한 함수들에 대해 알아보자.
</p><br/>

- abs(int형 데이터)
: 해당 데이터의 절대값을 반환하는 함수 
{% highlight ruby %}
abs(-3)
=> 3
{% endhighlight %}
<br/><br/>

- all( 반복 가능 자료형 )
: 반복 가능한 자료형( 리스트, 튜플, 문자열, 딕셔너리, 집합)을 인수로 받아<br/>
해당 자료형의 모든 데이터가 참이면 True를 반환하고, 하나라도 거짓이면 False를 반환
{% highlight ruby %}
all([1, 2, 3]) 
=> True 
all([1, 2, 0]) 
=> False
{% endhighlight %}
<br/><br/>

- any( 반복 가능 자료형 )
: all()과 반대로 하나라도 참일경우 True, 모두 거짓일 경우 False를 반환
<br/><br/>

- chr(아스키코드값)
: 아스키코드값을 인자로 받아 해당 아스키 코드에 해당하는 문자를 반환
{% highlight ruby %}
chr(97) 
=> 'a'
{% endhighlight %}
<br/><br/>

- ord( 문자)
: 해당 문자의 아스키코드값을 반환
{% highlight ruby %}
ord('a') 
=> 97
{% endhighlight %}
<br/><br/>

- dir( 데이터 )
: 해당 데이터 자료형, 또는 객체가 가지고 있는 관련함수를 보여준다.
{% highlight ruby %}
dir([1,2,3]) 
=> [ "append', 'count', 'extend', ... ]
{% endhighlight %}
<br/><br/>

- divmod( a, b)
: 두개를 인자로 받아 a를 b로 나눈 몫과 나머지를 튜플로 반환하는 함수
{% highlight ruby %}
divmod(7,3) 
=> (2,1)
{% endhighlight %}
<br/><br/>

- enumerate( 순서가 있는 자료형 )
: 인덱스가 있는 자료형( 리스트, 튜플, 문자열 )을 인자로 받아,<br/>
인덱스번호와 데이터를 가지고 있는 enumerate객체로 반환해준다. => for문 등에서 자주 사용된다.
{% highlight ruby %}
for i, name in enumerate( ['body', 'foo', 'bar' ] ) :
	print(i, name)
=> 
0 body 
1 foo
2 bar
{% endhighlight %}
<br/><br/>

- filter( 함수이름, 반복가능 데이터 )
: 반복가능 데이터를 해당 함수에 하나씩 대입하여 리턴값이 참인 경우에만 반환해줌.<br/>
=> for문 등에서도 사용이 가능하다.
{% highlight ruby %}
def positive(x) :
	return x>0

list(filter(positive, [1, -3, 2, 0, -5] ) ) 
=> [ 1, 2 ]
{% endhighlight %}
<br/><br/>

- map( 함수이름, 반복가능 데이터 )
: 동작원리는 filter와 비슷하지만, map은 boolean데이터형을 리턴해 준다.
{% highlight ruby %}
def positive(x) :
	return x>0

for i in map(positive,[1, -3, 2, 0, -5]) :
    print(i)

실행결과 => 
True
False
True
False
False
{% endhighlight %}
<br/><br/>

- hex( 정수 )
: 16진수로 리턴해줌 
{% highlight ruby %}
hex(234) 
=> '0xea'
{% endhighlight %}
<br/><br/>

- id( 객체 )
: 해당 객체의 주소값(레퍼런스)를 리턴
<br/><br/>

- isinstance( 객체, 클래스 )
: 해당 객체가 해당 클래스의 것인지를 판단하여 불리언리턴
<br/><br/>

- max( 반복가능 자료형 )
: 최대값 리턴
<br/><br/>

- min( 반복가능 자료형 )
: 최소값 리턴
<br/><br/>

- oct(정수)
: 8진수반환
<br/><br/>

- pow(정수1, 정수2)
: 정수1의 정수2제곱한 결과를 리턴
<br/><br/>

- round(실수)
: 해당 실수를 반올림해서 리턴
<br/><br/>

- sorted ( 반복가능 자료형 )
: 해당 데이터를 정렬하여 리스트로 리턴<br/>
( .sort() 는 값을 반환하지 않기 때문에 저장이 불가능 하지만 sorted()는 저장이 가능하다. )
{% highlight ruby %}
a = [1, -3, 2, 0, -5]
sorted(a)
print(a)
a.sort()
print(a)

실행결과 =>
[1, -3, 2, 0, -5]
[-5, -3, 0, 1, 2]
{% endhighlight %}



<br/>