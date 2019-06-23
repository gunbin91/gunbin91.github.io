---
layout: post
title: "1. 자바스크립트(JavaScript)"
tags: [ javascript ]
date: 2019-05-24
categories: [ javascript ]
---

<p align="center">
    자바스크립트(정식명칭은 ECMAScript)는 웹 개발자가 반드시 알아두어야 하는 프로그래밍 언어이다. 
</p><br/>

# ◆ 자바스크립트 (JavaScript)
DB작업등의 기술적 작업은 백엔드에 속하고, css나 자바 스크립트 같은 디자인 관련 작업은 프론트엔드라 칭한다. 개발자는 보통 백엔드의 작업을 하지만, 자바스크립트는 개발자의 영역이다.

<br/>

#### ▶ 자바스크립트의 특징  
- 자바스크립트를 이용하면 <font color="orange">HTML의 자체 변화를 일으키게 유도</font>할 수 있다.<br/> 해당 HTML파일에 자바스크립트를 섞어서 전송하게 되면 새로운 HTML을 보내지 않아도 해당 페이지 내의 자체 변화를 일으키게 유도할 수 있다.

<br/>
- 자바스크립트는 &lt;script>~&lt;/script> 안에 작성한다.

<br/>

#### ▶ 간단예시
{% highlight ruby %}
<img src="/assets/img/portfolio/cabin.png" id="img" onmouseover="overChangeImg();" style="width:500px;height:200px;">

<script>
    function overChangeImg(){
        document.getElementById("img").src="/assets/img/portfolio/cake.png";
    }
    function leaveChangeImg(){
        document.getElementById("img").src="/assets/img/portfolio/cabin.png";
    }
</script>
{% endhighlight %}
<h4>▼아래 이미지에 마우스를 올려보세요</h4>
<img src="/assets/img/portfolio/cabin.png" id="img" onmouseover="overChangeImg();" onmouseleave="leaveChangeImg();" style="width:500px;height:200px;padding:0;">

<script>
function overChangeImg(){
    document.getElementById("img").src="/assets/img/portfolio/cake.png";
}
function leaveChangeImg(){
    document.getElementById("img").src="/assets/img/portfolio/cabin.png";
}
</script>

<br/>

# ◆ 자바스크립트의 기본 문법
#### ▶ 자바스크립트 <font color="orange">변수의 선언은 모두 var</font>로 선언한다.
ex ) var x, y, z;
- 선언은 var로 하지만 변수에 <font color="orange">들어있는 값에 따라 타입이 달라질 수 있다.</font>
- 변수의 타입은 'typeof 변수'해당 변수의 타입을 확인할 수 있다.
- 변수에 숫자를 집어넣게 되면 변수의 type은 number이 되지만, 해당 변수에 다시 true란 값을 넣게 되면 type은 boolean으로 바뀌게 된다.
- 단, 변수의 값이 없는 경우 undefined가 되고, undefined는 자바의 null과 비슷한 용도로 사용된다. 

<br/>

#### ▶ 자바스크립트에는 char형이 없기 때문에 문자열 표기를 할 때, 쌍 따옴표나 홑 따옴표 둘 다 string형으로 인식한다. 즉, 둘 다 써도 상관이 없다.

<br/>

#### ▶ 코드는 순차적으로 진행. ( 따라서, 보통 메서드로 정의 해두고 쓰인다. )
#### ▶ 주석 처리는 java와 동일. ( // , /**/ ) 
#### ▶ 기본형 타입은 boolean, number, string
( 자바스크립트에도 null은 있음 )

#### ▶ 자바스크립트에는 기본형 데이터가 없다. ( =모두가 객체)
ex ) true.toString(), 47.4265.toFixed(2) 등등 모든 데이터 값을 객체로 인식함.<br/>
=> toFixed(2)는 소수점 두 번째 자리까지 끊도록 변경
#### ▶ 기본 연산 작업(산술, 비교, 대입)은 자바와 대체로 동일하다.
#### ▶ <font color="orange">메서드는 function으로 선언</font>한다. 또한 <font color="orange">반환형을 적어주지 않고, 매개변수 앞에 자료형을 쓰지 않는다.</font>
ex ) function A( num ){ }
- 호출할 때는 A( 2 ), A(true), A("바보") 등 다양한 형태의 자료형을 넣어도 되고,
여러 개의 인자를 보내도 상관없지만, 맨 처음 인자만 인식한다.
- 태그 안에서 on옵션에 인자를 넘길 때는 홑 따옴표 안에 쓰도록 한다.<br/>
 ( 쌍 따옴표랑 겹치기 때문에 )
#### ▶ 자바스크립트에서 for문도 가능하지만, <font color="orange">확장 for문은 불가</font>
확장포문 : for( String s : ar ) 불가
#### ▶ HTML태그의 onclick등의 스크립트메서드를 호출하는 옵션에서는 스크립트언어로 적용되기 때문에 window.alert()등 한 줄짜리 메서드는 굳이 스크립트로 만들지 않아도 호출이 가능하다.

#### ▶ number타입은 정수와 실수를 구분하지 않으므로 숫자의 나누기 연산은 몫을 구하는 것이 아닌 해당 나누기 값을 구한다.
ex ) 14/3 = 4가 아닌 4.333333 이 나오게 된다. 
#### ▶ 자바스크립트의 <font color="orange">문자열비교는 equals가 아닌 ==</font> 로 한다.

<br/>

# ◆ 자바스크립트 기본 메서드
- console.log("내용");
: <font color="orange">f12 개발자도구</font>의 콘솔 탭에서 내용들을 볼 수 있게 해준다.( 테스트용으로 자주사용 )
- window.prompt("내용");
: String값을 <font color="orange">입력 받을 수 있는 창을 제공</font>한다. 매개인자의 내용은 화면에 보여줄 내용 - string반환<br/>
<button onclick="prompt('프롬프트창입니다^^');">prompt</button>
- window.alert("내용");
: 내용으로 <font color="orange">알림창</font>만 제공 <button onclick="alert('얼럿창입니다^^')">alert</button>
- window.confirm("내용");
: 예(true), 아니요(false) 버튼을 클릭할 수 있는 알림 창 - boolean반환<br/>
<button onclick="confirm('컨펌창입니다^^');">confirm</button>
- document.getElementById("아이디")
: 태그의 옵션으로 설정한 <font color="orange">아이디에 해당하는 태그객체</font>를 불러오는 메서드<br/>
=> '.옵션' 으로 해당 태그의 옵션 값이 무엇인지 뽑아낼 수 있고 수정도 가능하다.
- 아이디로 뽑아낸 객체.innerHTML 
: 태그(<>)와 끝맺음 태그(</>) 사이에 있는 <font color="orange">태그의 내용</font>을 객체로 뽑아낼 수 있다. <br/>
(value로 설정되어있지 않은 내용 ( div같은..))
- 체크박스객체.checked 
: 체크박스가 체크인지 아닌지 boolean 반환
- 폼객체.submit();   
:  폼의 submit버튼을 누른 것과 같은 액션
- window.setInterval(함수명,1000);
: 특정 함수를 ms단위 초 인자 값 당 한 번씩 호출<br/>
( 주의) 할 점은 함수는 () 없이 함수명만 쓴다. )<br/>
=> setInterval()함수가 호출된 횟수를 반환 ( 인자로 있는 함수의 호출횟수가 아님 )
- window.clearInterval( setInterval()이 반환한 값 )
: setInterval() 의 작업을 멈춤

<br/>

# ◆ Global속성 또는 Global함수
객체 지정 없이 전역으로 사용되는 속성이나 함수

▶ undefined 
: 값이 없는 변수에 들어가는 값 ( null과 비슷)
<br/> <font color="orange">a == undefined 로 비교가능</font>

▶ NaN
: Not a Number 숫자가 아닌 값을 반환할 때 나오는 값<br/>
=> == NaN 으로 비교가 불가능하고 <font color="orange">isNaN( a )으로 처리</font>해야한다.

▶ Infinity
: 무한 값을 의미 typeof 는 Number

▶ var e = encodeURI("가나다");
: utf-8로 변환

▶ var e = decodeURI(e);
: 다시 원래 문자로 재변환

▶ parseInt(n) 
: n을 int형으로 변환<br/>
( 자바의 Integer.parseInt() 와 다른 함수, 스트링 형 두개를 더하거나 할 때 사용 )

▶ parseFloat(n)
: n을 float형으로 변환<br/>
=> 자바스크립트의 형변환은 parseInt, parseFloat 밖에없다.

#### ▶ 스크립트에서 태그객체.click()를 하게 되면 해당 태그를 onclick()을 호출한 것과 같다.





<br/>