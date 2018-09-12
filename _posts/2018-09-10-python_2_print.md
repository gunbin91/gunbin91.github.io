---
layout: post
title: "2. 문자열과 출력"
tags: [ python, python string, python print ]
date: 2018-09-10
categories: [ python ]
---

<p align="center">
    파이썬에서 문자열을 표현하는 방식과 입/출력방식에 대해 알아보자.
</p><br/>

# 파이썬 문자열과 출력
파이썬에서 문자열은 <font color="orange">작은 따옴표(‘’), 큰 따옴표(“”), 따옴표 세 개(‘’’ 또는 “””)</font>로 표현할 수 있다.<br/>
- 따옴표 세 개로 문자열을 정의할 경우, 코드 상 여러 줄에 걸친 문자열을 쓸 때 사용한다.<br/>또한 줄 바꿈이 있을 경우 결과물에서도 줄 바꿈이 적용된다.
<br/><br/>
- 파이썬 문자열에서 모든 공백 문자 즉, 띄어쓰기나 탭 등은 입력한 그대로 유지된다.
<br/><br/>
- <font color="orange">str(정수)</font>함수로 <font color="orange">정수를 문자열로 변환</font>할 수 있다.
<br/><br/>
- 파이썬에서 문자열의 +연산은 문자열 끼리만 가능하다.<br/><font color="powderblue">문자열 + 문자열 = 가능</font><br/><font color="red">문자열 + 정수 = 불가능</font>
<br/><br/>

# 문자열 포맷팅
문자열 중간에 데이터를 삽입하고자 할 때 사용하는 <font color="orange">'문자열.format()'</font>함수를 알아보자.
<br/>
{% highlight ruby %}
age = 20
name = "Swaroop"
{% endhighlight %}
#### ▶ 위치 지정하여 삽입
print("<font color="orange">{1}</font> was <font color="orange">{0}</font> years old when he"<font color="orange">.format(age, name)</font>)
<br/>=> <font color="deeppink">Swaroop</font> was <font color="deeppink">20</font> years old when he

#### ▶ 순서대로 삽입
print("<font color="orange">{}</font> was <font color="orange">{}</font> years old when he"<font color="orange">.format(name, age)</font>)
<br/>=> <font color="deeppink">Swarrop</font> was <font color="deeppink">20</font> years old when he

#### ▶ 변수로 지정하여 삽입
print('<font color="orange">{name}</font> wrote <font color="orange">{book}</font>'<font color="orange">.format(name='Swaroop',book='A Byte of Python')</font>)
<br/>=> <font color="deeppink">Swaroop</font> wrote <font color="deeppink">A Byte of Python</font>
    
#### ▶ 소수점표기 ( 소수점 이하 자릿수 지정)
print('<font color="orange">{0:.3f}</font>'.format(1.0/3))
<br/>=> 0.333
> “어쩌구 %d 저쩌구”.%3 의 형식으로도 가능하다. ( %s, %f … )

#### ▶ 칸채우기
print('<font color="orange">{0:a^11}</font>'.format('hello')) 
<br/>=> aaa<font color="deeppink">hello</font>aaa
<br/>11자리 중 나머지를 'a'로 채우고 hello 가운데 정렬(^)<br/>
( 가운데정렬(^), 왼쪽 정렬(<), 오른쪽 정렬(>) )

#### ▶ 문자열,데이터 붙이기
print ('Area is', area, breadth, "aaa")<br/>
=> Area is (area값) (breadth값) aaa<br/>
python에서 <font color="orange">print문은 콤마(,)로 이어서 출력이 가능</font>하다. 문자열 뿐만 아니라 정수형 데이터 또한 가능


# print함수 줄바꿈 무시하기
print()함수는 자동으로 한번 출력 후 줄바꿈이 실행되는데, 이를 무시할 수도 있다.<br/>
단, python2와 python3간에는 약간의 문법차이가 있다.<br/>

- Python2 : 끝에 콤마(,)를 찍어 줄 바꿈을 막는다.<br/>
Ex ) print "a"<font color="orange">,</font>
- Python3 : ,end=””등을 이용하여 막는다.<br/>
Ex ) print("a"<font color="orange">,end = ""</font>)

> python2에서는 print를 괄호() 없이 사용하고, python3에서는 print()로 사용한다.<br/>
이 외에도 문법적인 차이가 조금씩 있기는 하지만 무엇으로 하든 공부하기에 큰 지장은 없다.

# 이스케이프 문자 무시하기
\n등의 줄바꿈 문자를 표기하는 <font color="deeppink">역슬래쉬로 사용하는 문자들을 이스케이프 문자</font>라고 하는데,<br/>
이를 화면상에 그대로 출력하고 싶을때 사용하는 방법이 있다.<br/>

{% highlight ruby %}
print(r"Newlines are indicated by \n")
=> Newlines are indicated by \n
{% endhighlight %}
문자열 앞에 <font color="orange">r을 붙이게 되면 이스케이프 문자를 무시</font>하고 문자열 그대로 출력하게 된다.

# 두 줄 이상의 문자열 표현
코드상 두 줄 이상의 문자열을 하나의 print문에 사용할때 쓰는 방법에 대해 알아보자.
<br/>

#### ▶ 명시적 행간 결합
{% highlight ruby %}
print("This is the first sentence. \
      This is the second sentence." )
{% endhighlight %}
코드상 하나의 명령문이 너무 길어질 때 사용하는 방법으로 <font color="orange">끝에 '\'를 붙이게 되면, 코드상으로는 여러 줄을 나타내지만 실질적으로는 한줄로 처리</font>하게 된다.<br/>
=> 즉, <font color="deeppink">원래 한 줄의 명령어를 여러 줄에 걸쳐 쓸 때 사용</font>
> 이 방법은 문자열 뿐만 아니라 <font color="deeppink">모든 명령어에서 동일하게 적용</font>된다.

- 또는 문자열의 경우에는 ''' ~ '''로 표현이 가능하다. 단, ''' 안에서 문자열을 사용할 경우 코드상의 줄바꿈이 그대로 실행되기 때문에 주의하도록 하자.

# 입력 받기
{% highlight ruby %}
변수 = input("표기할 문자 ")
{% endhighlight %}

사용자로 부터의 입력은 <font color="orange">input()함수</font>를 사용하여 받게된다.<br/> 해당 입력값이 함수의 반환값으로 반환되어 이를 변수에 저장할 수 있게된다.
> cf ) <font color="orange">int(input("표기할 문자"))</font>를 이용하면 입력과 동시에 형변환 또한 가능하다.<br/>
( raw_input() 메서드는 파이썬3에서는 사용불가 = 삭제됨 )

# 문자열 관련 함수 
- &nbsp;<font color="orange">len</font>(문자열) 
: 문자 또는 열거형 데이터의 길이를 int형으로 반환
{% highlight ruby %}
le = len("hello")
print(le)
=> 5
{% endhighlight %}

- 문자열1.<font color="orange">count</font>(“문자열2”) 
: 문자열1에 포함되어있는 문자열2의 개수를 int형 반환
{% highlight ruby %}
co = "wellcome to korea".count('o')
print(co)
=> 3
{% endhighlight %}

- 문자열1.<font color="orange">find</font>(“문자열2”) 
: 문자열1에서 문자열2를 찾아, 문자열1에서 문자열2가 시작되는 인덱스를 int형 반환
<br/>( 못 찾으면 -1 반환 )
{% highlight ruby %}
co = "wellcome to korea".find('to')
print(co)
=> 9
{% endhighlight %}

- 문자열1.<font color="orange">index</font>(“문자열2”)
: find()와 같은 기능을 하지만 못 찾을 경우 에러 발생
{% highlight ruby %}
co = "wellcome to korea".index('to')
print(co)
=> 9
{% endhighlight %}

- 문자열1.<font color="orange">join</font>(“문자열2”)
: 문자열2의 단어 사이마다 문자열1을 삽입
{% highlight ruby %}
st="/".join("abcd")
print(st)
=> a/b/c/d
{% endhighlight %}

- 문자열.<font color="orange">upper</font>()
: 대문자 변환
{% highlight ruby %}
up = "hello".upper()
print(up)
=> HELLO
{% endhighlight %}

- 문자열.<font color="orange">lower</font>() 
: 소문자 변환
{% highlight ruby %}
up = "HELLO".lower()
print(up)
=> hello
{% endhighlight %}

- 문자열.<font color="orange">lstrip</font>() 
: 왼쪽공백지우기, 
<br/>( rstrip()오른쪽, strip()양쪽 )


- 문자열.<font color="orange">split</font>(“문자열”) 
: 매개변수를 기준으로 기존 문자열을 나누고 리스트로 반환
{% highlight ruby %}
sp = "wellcome to korea".split(" ")
print(sp)
=> ['wellcome', 'to', 'korea']
{% endhighlight %}

# 파이썬 변수
파이썬은 <font color="deeppink">변수를 따로 선언하지 않고</font>도 바로 <font color="deeppink">대입과 동시에 변수가 선언됨</font>과 같은 역할을 한다.

- 파이썬 식별자(변수) 이름 규칙
: 앞 문자는 알파벳(대/소) 혹은 언더바( _ ) 나머지는 문자, 언더바( _ ), 숫자

# 파이썬의 물리적 명령 행과 논리적 명령 행
- &nbsp;<font color="deeppink">물리적 명령 행</font> : 프로그램 코드 내의 한 줄
- &nbsp;<font color="orange">논리적 명령 행</font> : 인터프리터가 인식하는 한 명령의 단위

> 하나의 물리적 명령 행에 두 개의 논리적 명령 행을 넣게 될 경우 오류로 간주한다.
<br/> 따라서 파이썬에서는 세미콜론(;)을 사용하지 않지만 <font color="orange">이 경우에는 세미콜론으로 구분 지어 사용</font>한다.

> 단, <font color="deeppink">파이썬에서는 세미콜론을 허용</font>하기 때문에 명령어 끝에 세미콜론을 써도 되지만 권장사항은 아니다.





<br/>