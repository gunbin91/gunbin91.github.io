---
layout: post
title: "4. 객체제어 및 쿠키"
tags: [ javascript cookie ]
date: 2019-05-25
categories: [ javascript ]
---

<p align="center">
    스크립트의 여러 사용방법과 쿠키를 스크립트로 제어하는 방법에 대해 알아보자
</p><br/>

#### ▶ 태그의 on옵션의 메서드를 스크립트에서 정의
태그의 on메서드 들은 속성에 바로 메서드를 지정하면 되지만, 스크립트에서 등록 할 수도 있다.
{% highlight ruby %}
document.getElementById("t2").onclick = function() {
    window.alert(this.value);
}
{% endhighlight %}
온 클릭 메서드를 스크립트 내에서 정의, 또는 변경도 가능하다.

<br/>

#### ▶ a 태그의 href 옵션에서 스크립트 함수 호출
a태그 클릭 시 href속성으로 설정된 경로로 이동되지만, 경로이동이 아닌 스크립트 메서드를 호출하고자 할 경우 아래와 같이 하면된다.
{% highlight ruby %}
<a href= "javascript:함수명()">
{% endhighlight %}
 
<br/>
 
#### ▶ 자바스크립트는 함수 또한 객체로 처리한다.
{% highlight ruby %}
// 함수를 변수에 저장할 수 도 있고
var t = function() {
    console.log("t");
}

// 함수를 콘솔로 찍을 수 도 있다. (type은 function )
function test() {
    console.log("test");
}
console.log(typeof test + " / " + test + " / " + t);
{% endhighlight %}

<br/>

#### ▶ 자바스크립트의 Object
- Object 객체 생성
: var o = new Object();
- 객체의 변수 선언
: o.age = 30;<br/>
=> console.log(o.age); 하게 되면 age값이 나오게 된다. <br/>
즉, o.age=30 과 동시에 변수가 만들어지고 값을 초기화 하게 되는 것( 선언과 동시 초기화 )
- 객체의 함수정의
: o.test = function(){ window.alert("ㅇㅇ");} <br/>
=> o.test()를 호출하게 되면 해당 함수가 나오게 된다. 즉, 위의 코드가 함수를 정의하는 것.<br/>
( 마찬가지로 함수 또한 선언과 동시에 정의가 된다. )
- 객체의 변수 사용
: o.test = function(){ window.alert(this.job); }<br/>
=> o.job을 통해서 정의한 변수를 사용하기 위해서는 해당 오브젝트 안에서 this 키워드를 사용한다.

<br/>

#### ▶ 자바스크립트의 객체(Object) 설계
{% highlight ruby %} 
var robot = function(i, q) {
    this.iq = i;
    this.name = q;
    this.greet = function() {
        alert("안뇽하쉐욜\nIQ " + this.iq + "인 " + name + "이라고 해용.");
    }
}

var r1 = new robot();
console.log(r1.iq);
r1.greet(); 
r2.greet = function(){
    window.alert("함수변경");
}
{% endhighlight %}
- 자바스크립트의 객체설계는 자바의 생성자와 비슷한 형식으로 한다.
- 인자를 두개 이상으로 하는 객체를 설계 시, new를 통해서 만든 객체의 인자는 없어도 되고, 하나만 있어도 된다.
- 자바스크립트의 객체에 설계된 함수는 변경도 가능하다.

<br/>

# ◆ 태그 객체의 사용
<br/>

#### ▶ this 키워드의 사용
{% highlight ruby %}
document.getElementById("t2").onclick = function() {
    window.alert(this.value);
}
{% endhighlight %}
위 예시처럼 스크립트에서 onclick을 등록할 경우 this키워드를 사용하여 해당 객체에 접근이 가능하다.

<br/>
하지만, 태그 내의 onclick메서드에서 호출한 메서드 내부에서는 this를 사용할 수 없다.<br/>
따라서 따로 정의된 메서드에서 해당 태그를 사용하고자 할 경우, id를 통해 뽑아내거나 onclick메서드에 메서드를 등록할 때 <font color="orange">인자로 this를 넘겨주어야 한다.</font>
{% highlight ruby%}
<input type=“button” onclick=“func(this);”>
{% endhighlight %}

<br/>
#### ▶ 태그의 속성변경
태그의 속성을 변경하고자 할 경우 해당태그에서 사용한 속성을 그대로 뽑아내어 대입연산자로 바꿔주기만 하면 된다.
{% highlight ruby %}
<a href="main.jsp" id="a">main</a>
<script>
document.getElementById("a").href = "sub.jsp";
</script>
{% endhighlight %}

<br/>

#### ▶ style속성의 옵션은 스타일객체를 타고 들어가서 확인한다.
style속성 내부에는 css가 관장하는 또 다른 속성들이 있기 때문에 속성을 두번에 걸쳐 타고들어가서 확인/수정 할 수 있다.
{% highlight ruby %}
document.getElementById("id").style.color = "green";
{% endhighlight %}

<br/>

#### ▶ boolean 형태로 반환하는 태그의 옵션
checked, disabled, readonly 해당 옵션들은 string으로 반환되는 것이기 아니기 때문에 변경 시 true/false로 바꿔주어야 하고, 반환 또한 true/false로 반환한다.<br/>

또한 boolean형태로 반환되는 옵션들은 태그에서 설정할 때 = 을 통해 값을 설정하는 것이 아니고, checked라고 그냥 써주기만 하면 된다.<br/>
<b>ex ) &lt;input type="radio" checked></b>

<br/>

# ◆ document.cookie 객체 (쿠키)
document객체는 HTML요소 제어뿐만 아니라, 쿠키도 제어할 수 있다.

<br/>

#### ▶ 쿠키 반환
{% highlight ruby %}document.cookie{% endhighlight %}
를 하게 되면, JSESSION을 제외한 모든 쿠키들이 <font color="orange">'쿠키네임=쿠키값;' 형태로 스트링형</font>으로 뽑히게 된다. 
<br/>=> 따라서, split(";")로 분리해서 사용이 가능하다.

<br/>

#### ▶ 쿠키의 생성
{% highlight ruby %}
document.cookie = "pop=true"; 
{% endhighlight %}
document.cookie는 스트링형태로 전체 쿠키를 반환하지만,<br/>
쿠키를 집어넣을 때는 += 으로 이어 붙이는게 아니라, <font color="orange">document.cookie="쿠키네임=쿠키값";</font> 한 줄로 쿠키가 하나 추가된다.

<br/>

#### ▶ 쿠키의 경로 설정
{% highlight ruby %}
document.cookie = "cok" + "=" + Math.random() + "; path=/chap07";
{% endhighlight %}
쿠키 생성 시, <font color="orange">세미콜론(;) 뒤에 path=경로</font>를 붙여서 쿠키의 경로를 설정할 수 있다.

<br/>

#### ▶ 쿠키의 유효시간 설정
{% highlight ruby %}
document.cookie = 
"cok" + "=" + Math.random() + "; path=/chap07; expires="+ new Date("2018-01-25").toGMTString();
{% endhighlight %}
쿠키의 유효시간을 설정하기 위해서는 <font color="orange">'expires = Date객체의 toGMTString()메서드'</font>를 이용하여 설정을 해야한다.
<br/>

Date객체의 toGMTString() 메서드를 찍게되면 =>
Thu Jan 25 2018 09:00:00 GMT+0900 (대한민국 표준시) 
형태로 나오기 때문에 직접 써서 사용 하는 것이 어렵다.
<br/>따라서 데이트객체를 이용하여 설정한다.
또한, 자바에서는 쿠키의 생존시간을 초로 설정하지만, 스크립트에서는 쿠키의 만료기간을 정하는 것이다.
{% highlight ruby%}
하루설정 ex ) 
new Date(Date.now() +1000*60*60*24).toGMTString();
{% endhighlight %}

<br/>

#### ▶ 쿠키 제거
{% highlight ruby %}
document.cookie = "cok=; path=/chap07; expires="+ new Date(0).toGMTString();
{% endhighlight %}
해당 쿠키의 유효시간설정을 0 로 해두면 된다.

> 쿠키는 전역에서 사용하는 것이기 때문에 <% ~ %> 에서도 사용이 가능하다.






<br/>