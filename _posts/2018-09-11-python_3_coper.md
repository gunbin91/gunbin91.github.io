---
layout: post
title: "3. 연산자 및 흐름제어"
tags: [ python, python if, python for ]
date: 2018-09-11
categories: [ python ]
---

<p align="center">
    파이썬의 연산자 기능과 흐름제어에 대해 알아보자.
</p><br/>

# 파이썬의 연산자와 수식
다른 언어들과 다른 연산자 수식에 대해 살펴보도록 하자.
<br/>

#### ▶ 문자열 곱셈
파이썬에서는 문자열에 곱셈연산을 할 수 있다. 기능은 <font color="deeppink">문자열 덧셈을 여러번 한 것</font>과 같다.
{% highlight ruby %}
print('la' * 3)
=>'lalala'
{% endhighlight %}
<br/>

#### ▶ ** 연산자
&nbsp;<font color="deeppink">**</font>연산자는 <font color="deeppink">거듭제곱</font>의 기능을 표현하는데 사용한다.
{% highlight ruby %}
print(3 ** 4)
=> 81
{% endhighlight %}
(이 값은 3 * 3 * 3 * 3 과 같습니다). 즉, 3의 4승
<br/>

#### ▶ 논리 연산자
-	'&&', '<font color="black">||</font>', '!' 대신 <font color="orange">and</font>, <font color="orange">or</font>, <font color="orange">not</font>를 사용함
-	boolean데이터 :  <font color="orange">True</font>, <font color="orange">False</font> ( 앞 문자가 대문자)
<br/>

#### ▶ 나머지를 버리는 // 연산
{% highlight ruby %}
print(7 // 4) 
=> 1
print(7 / 4)
=> 1.75
{% endhighlight %}
즉, <font color="deeppink">몫만 구하는 연산자</font><br/>
( 파이썬에서 '/' 연산자는 소수점 까지 계산하여 반환한다. )

> 파이썬도 마찬가지로 +=, *= 등의 연산자들은 다른언어들과 동일하게 작동한다.
<br/>

# 파이썬의 흐름제어

### ▶ if문
{% highlight ruby %}
if 조건 :
elif 조건:
else :
{% endhighlight %}
> cf) 파이썬은 switch문이 없음 

<br/>

### ▶ while문
{% highlight ruby %}
while 조건 :
{% endhighlight %}
> True와 False는 int형으로 변환 시 0 또는 1로 변환<br/>
즉, True == 1은 True를 반환

<br/>

### ▶ for문
{% highlight ruby %}
for 변수 in 리스트 :
{% endhighlight %}

# range()
for문과 자주 같이 쓰이는 함수로, 리스트를 만들어준다.
- for i in range(1, 5) 
: for i in [1, 2, 3, 4] 와 같다<br/>
즉 range(1,5) 는 1이상 5미만 리스트 반환.<br/>
위 for문은 i에 1부터 5까지 차례대로 대입시켜 반복시키는 흐름이다.

- range(1,5,2) 
: 1이상의 2씩 증가하는 5미만 리스트 반환

# ▶in , not in 리스트, 튜플, 문자열
해당 자료형 데이터 안에 있는지 없는지 검사
{% highlight ruby %}
‘j’ not in ‘python’ 
=> True
{% endhighlight %}

> break문 continue문도 사용이 가능하다.

# ▶ pass키워드
아무 기능을 하지 않고 넘어갈 때 사용, <br/>
이 기능은 보통 if, else등에서 아무것도 넣지 않을 시 오류를 발생시킬 수 있으므로 그 때 사용한다.




<br/>