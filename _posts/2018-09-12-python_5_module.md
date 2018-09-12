---
layout: post
title: "5. 모듈"
tags: [ python, python module ]
date: 2018-09-12
categories: [ python ]
---

<p align="center">
    하나의 파이썬 파일을 의미하는 모듈에 대해 알아보자.
</p><br/>

# 모듈( Module )
모듈은 하나의 코드작성 파일을 의미하며, 자바와 마찬가지로 import하여 재사용 할 수 있다.
<br/>

# 모듈을 만드는 방법
모듈을 만드는 가장 간단한 방법은 <font color="orange">‘.py’확장자를 가진 파일을 하나 만들고</font> 그 안에 함수들과 변수들을 정의해 두는 것이다 또는 <font color="deeppink">다른 언어(C)로 만들어진것 또한 import가 가능</font>하다.
<br/><br/>

# sys, os 모듈
파이썬에는 <font color="deeppink">기본적으로 내장되어 있는 모듈</font>이 있다. 그중에 sys, os 모듈은<br/>
시스템, 운영체제에 관한 함수들을 저장하고 있는 모듈로, 모듈을 import하는 방법은 <font color="orange">import sys,os</font>의 형식을 사용하여 불러온다.<br/>

- sys.argv 
: py파일을 실행할 때 들어오는 인자를 리스트로 반환<br/>
console :
~~~ 
python hello.py we are the one
~~~
=> sys.argv[0]부터 차례대로 hello.py, we, are, the, one가 들어간다.

- sys.path
: 파이썬 코드에서 import 할 때 불러올 모듈을 찾게 되는 디렉토리의 리스트가 담겨있다.<br/>
즉, <font color="deeppink">import할 모듈은 반드시 sys.path경로에 포함되는 디렉토리에 만들어야 한다.</font><br/>

> 또는 sys.path.append(“모듈이 있는 경로”)로 추가하여 모듈을 import할 수 있게 만들 수도 있다.

- os.getcwd()
: 현재 프로그램에서 <font color="orange">현재 디렉토리 경로를 스트링으로 반환</font>
<br/><br/>

# .pyc 파일
pyc파일은 바이트 컴파일된 파일로서, 일반 .py파일보다 가볍다. 따라서 모듈을 불러오는 작업은 상대적으로 무거운 작업이기 때문에 종종 <font color="deeppink">import할 파일을 .pyc확장자 파일로 작업하여 중간 단계의 파일로서 모듈을 불러오는 작업을 빠르게 수행</font>할 수 있게 한다.
<br/><br/>

# from ... import 문
모듈 전체를 import하지 않고 해당 <font color="deeppink">모듈내의 특정 부분만 import</font> 할 수 있도록 해주는 키워드로 <font color="orange">'from 모듈명 import 사용할객체'</font>로 불러온다.<br/>
또한 모듈내의 함수를 사용하기 위해서는 '모듈.함수'의 문법으로 호출해야 하지만, 'from 모듈 import 함수'로 불러올 경우 해당 함수를 <font color="deeppink">모듈이름 없이 바로 호출할 수 있게 된다.</font>

{% highlight ruby %}
from sys import argv 
{% endhighlight %}

- sys모듈의 argv함수를 사용할 수 있다. ( argv 만으로 )<br/><br/>
- 함수의 경우 ()없이 이름만 작성, 콤마(,)를 구분자로 여러 개를 import할 수도 있다.<br/><br/>
- from mymodule import * 로 해당 모듈의 전체를 불러올 수 있지만 이렇게 할 경우 '_ _ 속성 _ _' 등의 속성은 불러와지지 않는다. <br/><br/>
<br/><br/>

# 모듈의 name 속성
'_ _ name _ _' 을 하게 되면 <font color="orange">현재 모듈의 이름을 반환</font>해 주는데,<br/>
~~~
this.__name__
~~~
을 통해 해당 속성(_ _ name _ _)이 '_ _ main _ _'이라면 import되지 않고 바로 실행한 것이고,<br/> __main__이 아닌 다른 이름 이라면 모듈의 이름이 된다. 따라서 해당 사항을 검사하는 흐름제어를 만들 수 있다.
<br/><br/>

# 새로운 모듈 작성하기 
확장자 py 또는 pyc파일 모두 모듈이라고 하기 때문에 모듈을 작성하는 방법이 정해져 있지는 않다.

ex ) < module.py >
{% highlight ruby %}
def say_hi():
	print('Hi, this is mymodule speaking.')
__version__ = '0.1'
{% endhighlight %}
라는 모듈을 작성했을 때
< 실행코드 ><br/>
{% highlight ruby %}
import mymodule
mymodule.say_hi()
print('Version', mymodule.__version__)
{% endhighlight %}
등으로 사용할 수 있다.
<br/><br/>

# dir 내장 함수
객체에 정의되어 있는 식별자들의 목록을 불러올 수 있다.<br/>
즉, <font color="orange">모듈에서 사용할 수 있는 변수나 함수등의 이름을 리스트형으로 반환</font>해준다.<br/>

- dir( 객체명 ) 
: 해당 객체의 식별자들의 목록을 반환 ex ) dir(sys)

- dir() 
: 현재 모듈의 식별자들의 목록을 반환

- <font color="orange">del 객체변수</font><br/> 
현재 모듈의 해당 변수 식별자를 제거  <br/>
즉, del이라는 명령어는 <font color="orange">프로그램상에서 데이터를 완전히 삭제</font>해 버릴 수 있는 명령어이다.
{% highlight ruby %}
li = ['a','b','c']
print(li)
del li[0]
print(li)

실행결과
['a', 'b', 'c']
['b', 'c']
{% endhighlight %}

# 패키지
파이썬에서도 패키지의 개념이 적용되며, 
패키지 안에 하나의 py파일 이상이 있으면 <font color="deeppink">'_ _ init _ _.py'</font> 라는 특별한 파일이 패키지 안에 자동적으로 생성된다.<br/>따라서 해당 파일이 패키지 안에 존재 해야지만 파이썬 패키지로 인식되고, import할 수도 있다.



<br/>