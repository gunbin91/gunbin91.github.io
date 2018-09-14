---
layout: post
title: "1. Python ?"
tags: [ python, 파이썬 ]
date: 2018-09-10
categories: [ python ]
---

<p align="center">
    프로그래밍 언어중 하나인 Python은 초보자들이 접근하기 쉬운 언어중 하나이다.
</p><br/>

# 파이썬(Python)
인터프리터언어의 한 종류로 무료이며, 오픈소스 등이 많고 이식성이 좋다.
<br/>또한 어렵지 않은 문법을 가지고 있어 초보자들이 처음 접하기 좋은 언어로 알려져있다.

# 파이썬과 다른 언어의 차이
- 파이썬은 복잡하고 <font color="deeppink">반복적인 연산이 많은 프로그램과는 어울리지 않는다.</font> 하지만 다른 언어로 만든 프로그램을 파이썬 프로그램에 포함 시킬 수 있기 때문에 반복연산이 많고 빠른 실행속도를 요구하는 부분은 다른 언어로 대체가 가능하다.
> 때문에 파이썬 라이브러리 중에는 순수 파이썬이 아닌 C로 만들어진 것들도 많다.
- 단락을 구분하는 <font color="deeppink">중괄호({})를 사용하지 않는다.</font> ( 들여쓰기를 통해 구분)
- 가독성을 위한 들여쓰기를 하지 않을 시 실행이 되지 않는다. ( 즉 <font color="deeppink">들여쓰기는 필수</font> )
- 코드가 매우 간결 하기때문에 개발 속도가 빠르다.
- 명령어의 끝에 <font color="orange">세미콜론(;)을 쓰지 않는다.</font>

# 파이썬 설치
- window일 경우 <a href="http://www.python.org/downloads">http://www.python.org/downloads(파이썬 공식 홈페이지)</a>에 접속하여 맨 위 상단의 python최신 버전을 다운로드 한 후 인스톨러를 실행하여 맨 밑 <font color="orange">Add python 3.6 to PATH 옵션을 체크</font>해 주어야 어느 곳에서든 실행이 가능해진다.
- Linux의 경우에는 python이 기본적으로 설치되어 있다.

# 파이썬 실행 및 종료
 
파이썬 인터프리터 <font color="orange">실행</font>은 <font color="orange">python 3.6(32-bit)</font>를 실행 or cmd창에서 <font color="orange">'python'을 입력</font>하면<br/> 인터프리터라는 화면이 나오게 된다.<br/><br/>
<img src="{{site.baseurl}}/assets/post_img/python.jpg" style="padding:0;margin:0;">
- (> > >)는 ‘프롬프트’라 하며 명령어를 입력할 수 있는 하나의 행을 의미한다.
- <font color="orange">종료</font>는 <font color="orange">‘ctrl+z’</font>엔터 또는 <font color="orange">'> > > import sys > > > sys.exit()'</font> 로 종료가 가능하다.
> 인터프리터는 한 행의 명령어를 실행하여 바로바로 확인할 수 있는 콘솔이며, 인터프리터가 실행되는 동안의 명령어들 또한 축적되어 실행되게 된다. 실제로 프로그래밍을 할때는 에디터를 이용하여 작성한다.

# 파이썬 기초 문법 예제
인터프리터를 실행하여 기초문법을 하나씩 테스트 해보도록 해보자.<br/>
아래 예시들은 맛보기이며 자세한 내용은 다른 장에서 살펴볼 것이다.

#### ▶ 사칙연산
{% highlight ruby %}
>>> 1+2
3
{% endhighlight %}
<br/>

#### ▶ 변수에 대입
{% highlight ruby %}
>>> a = 1
>>> b = 2
>>> a+b
3
{% endhighlight %}
파이썬은 위처럼 변수를 선언할 때 <font color="deeppink">변수의 타입을 지정해주지 않고 변수명만으로 선언</font>을 한다.
<br/><br/>

#### ▶ 출력
{% highlight ruby %}
>>> a = 'Python'
>>> print(a)
Python
{% endhighlight %}
변수에는 문자도 대입할 수 있으며, 출력은 print(출력할 데이터)를 이용하여 출력한다.<br/>
또한 인터프리터에서는 print없이 a(변수)만 입력해도 출력된다.
<br/><br/>

#### ▶ 조건문 if
{% highlight ruby %}
>>> a = 3
>>> if  a>1 :
…	print(“a is greater than 1”)
…
a is greater than 1
{% endhighlight %}
a가 1보다 크다면 print내용을 실행하는 코드이다.<br/>
다른 언어들과 다르게 중괄호({})를 사용하지 않고 <font color="deeppink">':'를 시작으로 들여쓰기로 구분</font>하고,<br/> 앞에 <font color="deeppink">…은 아직 문장이 끝나지 않았음을 의미</font>하며, 다음 …이후 엔터를 누르면 해당 구문을 빠져나간다.<br/>
단, ...은 인터프리터화면에서만 표기되며 <font color="deeppink">실제 코드작성할때는 들여쓰기로 구분</font>한다.
<br/><br/>

#### ▶ 반복문 for
{% highlight ruby %}
>>> for a in [1, 2, 3] :
… 	print(a)
…
1
2
3
{% endhighlight %}
for a in[1, 2, 3]의 뜻은 a변수에 1,2,3을 차례대로 대입하여 반복시키는 것을 의미한다.<br/>
참고로 print()는 개행이 자동적으로 적용된다.<br/>
cf) while i<3 : 의 뜻은 i가3보다 작을 때 까지 반복
<br/><br/>

#### ▶ 함수
{% highlight ruby %}
>>> def sum(a, b) :
…	return a+b
…
>>> print(sum(3,4))
7
{% endhighlight %}
파이썬에서는 <font color="orange">def라는 예약어를 이용하여 함수를 만든다.</font><br/>위 코드는 변수 두 개를 인자로 받아 두 인자를 서로 더하여 반환하는 sum이라는 함수를 만들어내는 코드이다.<br/><br/>

#### ▶ 주의 할 점
- 파이썬에서는 들여쓰기를 필수적으로 해야하기 때문에 if문 등의 안에서 코드를 입력할 때 <font color="orange">들여쓰기의 의미</font>로 <font color="orange">'tab'키</font> 또는 <font color="orange">'스페이스바4칸'</font>을 해 주어야한다.<br/>
(이는 매우 번거로운 작업이므로 자동으로 들여쓰기를 해주는 에디터 사용을 추천한다. )<br/>
- <font color="deeppink">파이썬은 대소문자를 구분</font>하기 때문에 print를 PRINT등으로 쓸 경우 인식하지 못한다.
<br/>

# 파이썬 에디터
파이썬 설치 시 기본적으로 설치되는 <font color="deeppink">IDLE(Python 3.6 32-bit)</font>를 실행하게 되면 ‘IDLE 쉘’창이 나타난다.<br/>
파이썬 인터프리터와 기본적으로 같은 기능을 하지만, 차이점은 <font color="deeppink">들여쓰기와 가독성을 높여주는 글자 색을 자동으로 입혀주는</font> 차이가 있다.

#### ▶ 파이썬 파일 만들기 
파이썬 파일을 만들기 위해서 IDLE쉘 창에서 <font color="orange">‘File – New File’</font>을 누르게 되면 파이썬 코드를 수정할 수 있는 에디터 툴이 나오게 된다.<br/>
파일을 만들어 작성할 경우 <font color="deeppink">인터프리터와 달리 코드를 모두 작성한 후에 코드가 실행</font>된다. 즉 실제 프로그래밍을 할 시 파일을 만들어 작성해야 한다.<br/>
- 코드 작성 완료 후 <font color="orange">‘Run – Run Module’</font>를 누르게 되면 파일을 저장하게 되고 .py 확장자를 가진 파일이 생성된다. 동시에 IDEL쉘 창에 바로 실행 결과가 나오게 되며, 에디터 파일에서 F5입력 시 다시 한 번 결과가 나오게 된다.

#### ▶ 파이썬 파일 실행
파이썬언어로 작성한 파이썬파일(.py)를 실행하는 방법은 <font color="orange">명령 프롬프트 실행 ( 윈도우+R–>cmd)</font>후 에디터 파일로 만든 <font color="orange">파이썬파일 경로로 이동( cd … )</font>후 <font color="orange">‘python 파일명.py’</font>를 입력하게 되면 해당 에디터파일의 결과가 나오게 된다.<br/>

#### ▶ 파이썬 주석
주석은 프로그램에 전혀 영향을 주지 않는 설명을 달아주는 기능을 하는 것으로,<br/>
한 줄 짜리 주석을 처리하는 구문과, 여러줄을 묶어서 처리하는 구문이 있다.
- 한 줄짜리 : <font color="orange">‘#’</font>으로 시작하는 줄
- 여러 줄짜리 : <font color="orange">''' ~ '''</font> or <font color="orange">""" ~ """</font>

# 여러 다른 에디터
IDLE에디터는 파이썬에서 기본적으로 제공되는 에디터로 공부하기에는 적합하지만, 실무적으로는 여러가지 기능을 지원해주는 다른 에디터 등을 쓰는것이 좋다.
- 파이참
- 에디트 플러스
- 노트패드
- 서브라임 텍스트3
- Atom

# 파이썬 웹프로그래밍을 위한 프레임워크
최근 많은 홈페이지들이 파이썬으로 제작되고 있다. 파이썬으로 웹 프로젝트를 만들기 위해 사용하는 
대표적인 프레임워크로는 <font color="deeppink">'Flask', 'Django'</font>등이 있다.



<br/>