---
layout: post
title: "Jinja 템플릿 문법"
tags: [ python, jinja, 파이썬 ]
date: 2018-09-14
categories: [ python ]
---

<p align="center">
    Jinja는 flask가 기본적으로 지원하는 템플릿엔진이다.
</p><br/>

# Jinja ( Flask 기본 템플릿 엔진 )
html코드 내에서 파이썬 백엔드에서 보내는 정보의 출력이나, html코드의 동적 제어등을 위해 사용하는 플라스크 기본 템플릿엔진이다.
<br>

- {%raw%}<font color="orange">{# ... #}</font>{%endraw%}  :  주석 정의
<br/><br/>

# {% raw %}{{ 변수 }}{% endraw %}
변수나 표현식의 결과를 출력하는 구분자<br/>
<br/>

ex ) test.py
{% highlight ruby %}
return render_template('test.html', msg=msg)
{% endhighlight %}
ex ) test.html
{% highlight ruby %}
{% raw %}
{{ msg }}
{% endraw %}
{% endhighlight %}
- 위와 같이 html파일로 데이터를 보내기 위해서는 <font color="orange">render_template()</font>함수를 이용하여 html파일을 출력할 때, <font color="orange">두번째 인자</font>로 데이터를 보내면 <font color="orange">중괄호 2개( { { } } )를 이용</font>하여 해당 데이터를 출력할 수 있다.
<br/><br/>

- 데이터는 하나뿐만 아니라, <font color="orange">콤마(,)를 구분자로 여러개를 보낼수도 있다.</font>

<br/><br/>

# {%raw%} {% ... %} {%endraw%}
if문,for문 등의 흐름 제어문을 할당하는 구분자
<br/><br/>

## for문 사용
for반복문을 사용하기 위해서는 {%raw%}'<font color="orange">{% for 개별요소 in 열거형데이터 %}</font>'{%endraw%}의 문법을 시작으로, 반복문이 끝나는 지점에 반드시 {%raw%}'<font color="orange">{% endfor %}</font>'{%endraw%}를 붙여주어야 한다.
<br/>
{% highlight ruby %}
{% raw %}
{% for item in navigation %}
<li><a href="{{ item.href }}">{{ item.caption }}</a></li>
{% endfor %}
{% endraw %}
{% endhighlight %}
<br/><br/>

## if문 
Jinja템플릿의 if는 <font color="orange">if</font>, <font color="orange">elif</font>, <font color="orange">else</font> 세가지 키워드로 구성할 수 있다.
<br/>
{% highlight ruby %}
{% raw %}
{% if <조건> %}
    <실행코드>
{% elif <조건> %}
    <실행코드>
{% else %}
    <실행코드>
{% endif %}
{% endraw %}
{% endhighlight %}
<br/>

# 형 변환
Jinja에서도 형변환이 가능하다. 파이썬 파일에서 데이터를 보낼 때 부득이하게 수정이 불가한 상황등이 있기 때문에 이럴경우 html파일에서 Jinja템플릿문법을 이용하여 형 변환 하여야 한다.<br/>
형변환의 방법은 출력데이터 뒤에 '<font color="orange">{ { 데이터 | 변환할자료형 } }</font>'을 붙이는 것이다.
<br/>

{% highlight ruby %}
{%raw%}
{{ number|int }} 
{% endraw%}
{% endhighlight %}
<br/><br/>

# 세 자릿수마다 콤마(,)추가
뒤에서부터 <font color="deeppink">세자리 마다 콤마가 찍혀 있는 숫자형식을 포맷팅</font>하기 위해 아래코드가 필요하다.<br/>
실수 또한 소수점 뒷자리 까지 적용된다.
{% highlight ruby %}
{% raw %}
{{'{:,}'.format(number[0])}}
{% endraw %}
{% endhighlight %}
<br/><br/>

# 공백 제거 / 공백 유지
Jinja는 기본적으로 데이터를 출력할 때 포함되어 있는 공백을 무시하지 않고 모두 출력한다.<br/>
따라서 아래 코드를 이용하여 공백을 제거 혹은 유지시킬 수 있다.
<br/>
{% highlight ruby %}
{%raw%}
{%- %}, {%+ %}, {% -%}
{%endraw%}
{% endhighlight %}
- <font color="orange">'+'가 붙은 쪽은 공백을 유지</font>시키고 <font color="orange">'-'가 붙은 쪽은 공백을 제거</font>하는 형식이다.

<br/>
