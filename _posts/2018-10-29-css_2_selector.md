---
layout: post
title: "2. 선택자(Selector)"
tags: [ css,  css_selector ]
date: 2018-10-29
categories: [ css ]
---

<p align="center">
css를 태그에 style옵션으로 주는것이 아닌 따로 지정할 때, 하나의 객체, 모든 태그, 여러객체.. 등등의 여러가지 방법으로 적용시킬 객체를 지정할 수 있는데, 이렇게 적용시킬 객체를 지정하는 것을 선택자라고 한다.
</p><br/>

# 선택자( selector )
해당 CSS문법을 어느곳에 적용시킬 지를 선택자로 구분한다.<br/> 선택자를 지정할 때 여러가지 방법이 있지만, 기본적인 방법으로는 크게 세 가지가 있다.<br/>

#### <font color="deeppink"> ▶ 태그로 선언</font>
태그를 선택자로 지정하고자 할 경우, 아무 처리없이 해당 태그명만 입력해주면 된다.<br/> 이렇게 태그로 선택자를 지정할 경우 <font color="deeppink">모든 해당 태그에 적용</font>된다.<br/>
ex )&nbsp;&nbsp; <font color="orange">li</font>{ align:center; }
<br/><br/>

#### <font color="deeppink"> ▶ id를 지정하여 적용</font>
태그에 id값을 지정해주고, css에서는 적용시키고자 하는 id앞에 '<font color="orange">#</font>'을 붙여 해당선택자가 id값임을 알려준다. id를 이용할 경우 하나의 객체에만 적용된다. <br/>
ex ) &nbsp;&nbsp; &lt;h1 <font color="orange">id</font>="id_name">아이디&lt;/h1> 
<br/> &lt;style><font color="orange">#id_name</font>{ }&lt;/style>
<br/><br/>

#### <font color="deeppink"> ▶ 클래스로 선언</font>
태그에 class속성을 지정해 주고 css에서는 클래스명 앞에 '<font color="orange">.</font>'을 붙여서 선언한다. 클래스를 이용하여 적용하는 경우 해당 클래스값을 가진 모든 객체에 해당css가 적용된다.<br/>
ex ) &nbsp;&nbsp; <font color="orange">.class_name</font>{ }
<br/><br/>

# 부모/자식 선택자
#### ▶ 객체 안의 객체
어떤 객체 안에 포함되어 있는 객체에만 css를 적용하고자 할 경우,<br/> <font color="deeppink">공백을 구분자</font>로 차례대로 선택자를 써주면 된다.
<br/>
<b>Ex ) ol태그 안에 속해있는 li</b>
{% highlight ruby %}
<style>
	ol li{
		속성
	}
    # ol태그 안에 포함되어 있는 모든 li태그에 적용된다.
</style>
{% endhighlight %}
<br/><br/>

#### ▶ 객체 안의 직계객체
객체안에 있는 모든 객체가 아닌, 해당 객체의 자식객체중 최상위 레벨에 해당되는 직계객체들에게만 적용시킨다. 직계 객체를 표현하고자 할 경우 <font color="deeppink">구분자는 '>'</font>를 이용한다.<br/>

<b>Ex ) ol태그 바로 안(직계)에만 속해있는 li를 선택자로</b>
{% highlight ruby %}
<style>
	ol>li{
		속성
	}
    # ol태그 안의 최상위레벨 li태그에만 적용
</style>
{% endhighlight %}
<br/><br/>

#### ▶ 여러개의 선택자를 동시에 설정
여러개의 선택자를 <font color="deeppink">','를 구분자</font>로 적용할 경우 같은 내용의 css를 동시에 적용시킬 수 있다.
<br/>
<b>Ex ) ul과 ol에 같은 속성을 적용</b>
{% highlight ruby %}
<style>
	ul,ol{
		속성
	}
    # 모든 ul태그와 ol태그를 지칭
</style>
{% endhighlight %}
<br/><br/>

# 가상 클래스 선택자 ( pseudo class selector )
가상클래스 선택자는 리스너와 같이 바로 적용되지 않고, 어떤 <font color="deeppink">액션이 생겼을 때 적용될 수 있는 선택자</font>를 가리킨다. 가상 클래스를 적용시키기 위해서는 선택자 옆에 <font color="orange">': 액션명'</font>을 써주면 가상선택자가 된다.

- 선택자:<font color="orange">link </font>
: 방문한 적이 없는 링크

- 선택자:<font color="orange">visited</font> 
: 방문한 적이 있는 링크 ( 보안상 문제로 일부 속성만 사용가능 )

- 선택자:<font color="orange">hover</font> 
: 마우스를 롤오버 했을 때

- 선택자:<font color="orange">active</font> 
: 마우스를 클릭했을 때

- 선택자:<font color="orange">focus</font>
: 포커싱 되었을 때
<br/><br/>

### 선택자 학습게임 
<a href="flukeout.github.io">flukeout.github.io</a><br/>
html태그로 표현된 객체중 움직이는 객체를 css선택자로 지정해 보는 게임형식
<br/>구글에 "CSS cheat sheet selector"를 검색하여 찾아볼 수 있다.

<br/>