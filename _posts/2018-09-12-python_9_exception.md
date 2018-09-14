---
layout: post
title: "9. 예외처리"
tags: [ python, python exception, 파이썬 ]
date: 2018-09-12
categories: [ python ]
---

<p align="center">
    코드상의 오류로 발생할 수 있는 예외에 대한 처리에 대해 알아보자.
</p><br/>

# try ~ except 문
발생한 예외를 잡아서 프로그램이 중지되지 않고, 작성한 코드 대로 이어나갈 수 있게 하는 오류 처리 구문으로, 자바에서는 try~catch문을 사용하지만 <font color="orange">파이썬에서는 'try ~ except'를 사용하여 예외처리</font>한다.
{% highlight ruby %}
try :
	text = input("Enter something-->")
except EOFError :
	print("Wh did you do an EOP")
except KeyboardInterrupt :
	print("You cancelled the.. ")
else :
	print("You entered {}".format(text))
{% endhighlight %}
- try문은 예외가 발생할 수 있는 사항들을 작성하는 곳이고,<br/>
except는 try문에서 예외 발생 시 잡아내는 구문으로 뒤에 잡아낼 예외 클래스를 써준다.<br/><br/>

- except문에서 예외 클래스를 명시하지 않을 경우, 모든 예외를 잡아낸다.
또한 추가적으로 try~except문에는 else문을 삽입하여 예외가 발생하지 않을 경우 작동 할 수 있도록 흐름제어가 가능하다.
<br/><br/>

# 예외 발생시키기 및 예외클래스 제어
&nbsp;<font color="orange">예외를 강제로 발생</font>시키기 위해서는 <font color="orange">'raise 예외 클래스()'</font>라는 키워드를 사용하며, 이때 예외클래스의 init메서드가 호출된다. 해당 <font color="orange">예외 객체는 'except 예외 클래스 as 객체 변수명'을 통해 제어</font>할 수 있게 된다.<br/>

{% highlight ruby %} 
try:
    text = input('Enter something --> ')
    if len(text) < 3:
        raise ShortInputException(len(text), 3)
except ShortInputException as ex :
    print ('ShortInputException: The input was ' + \
           '{0} long, expected at least {1}')\
        .format(ex.length, ex.atleast)
else:
    print ('No exception was raised.')
{% endhighlight %}
<br/><br/>

# 예외 클래스 만들기
예외 클래스를 직접 만들기 위해서는 <font color="orange">Exception클래스를 상속</font>받아서 만들어야 한다.<br/>
또한 raise를 통해 예외를 발생시킬 때 해당 클래스의 init메서드를 호출하게 되므로, 
init메서드를 정의하고 그 안에 'Exception._ _ init _ _(self)'를 호출해야한다.
{% highlight ruby %}
class ShortInputException(Exception):
    def __init__(self, length, atleast):
        Exception.__init__(self)
        self.length = length
        self.atleast = atleast
{% endhighlight %}
<br/><br/>

# Finally
예외처리 시 예외가 발생하던, 발생하지 않던 간에 무조건 실행 될 수 있게 하는 구문으로 파일 등을 닫거나 할 때 사용.<br/>

{% highlight ruby %}
try:
    f = open("poem.txt")
    while True:
        line = f.readline()
        if len(line) == 0:
            break
except IOError:
    print ("Could not find file poem.txt")
except KeyboardInterrupt:
    print ("!! You cancelled the reading from the file.")
finally:
    if f:
        f.close()
        print ("(Cleaning up: Closed the file)")
{% endhighlight %}
<br/><br/>

# with
&nbsp;<font color="orange">try~finally문에서 처리하는 일반적인 처리방식을 자동적으로 지원</font>해주는 문으로, enter, exit메서드에 의해 자동적으로 다루어질 수 있는 경우에만 사용할 수 있다.
{% highlight ruby %}
with open("poem.txt") as f:
 for line in f:
    print(line)
{% endhighlight %}
> with문은 파일처리나 DB처리등의 반복적으로 열고 닫는등의 작업을 할 때 유용하게 쓰일 수 있다. 위 예시같은 경우 with문을 진입하면서 open()하고 빠져나갈때 자동적으로 close()해주게 된다.


<br/>