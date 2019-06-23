---
layout: post
title: "2. 기본 객체( 자료형 )"
tags: [ javascript type ]
date: 2019-05-24
categories: [ javascript ]
---

<p align="center">
    앞서 말했듯 자바스크립트는 전부 객체이다. <br/>하지만 자바스크립트에도 다른 언어의 자료형 처럼 사용되는 객체들이 있다.
</p><br/>

# ◆ 자바스크립트의 String

#### ▶ 자바스크립트의 string객체의 길이는 .length 로 뽑아낸다. 
( 자바의 스트링은 length() )

#### ▶ 스트링객체의 메서드
- .chatAt(number a) 
: 해당 인덱스의 문자를 string 타입으로 반환<br/>
( 스크립트는 char형이 없기 때문에 문자열로 반환한다. )
- .charCodeAt(number a) 
:  해당 인덱스의 문자를 아스키 값으로 반환
- .indexOf("문자열") 
: 해당 문자열이 있는 인덱스 번호를 반환 <br/>
=> 없으면 -1 반환
- .lastIndexOf("문자열") 
: 끝에서부터 찾아낸 인덱스 번호
- .search("문자열") 
: indexOf랑 같음 ( 단, search는 정규식을 지원함 )<br/>
=> 자바스크립트의 정규식은 / / 사이에 쌍 따옴표 없이 표기 한다.(문자열로 표기하지 않음)<br/>
ex ) "javascript".search(/[abc]s/)); => 3을 반환 
- .includes("문자열") 
: 해당 문자열 내용을 포함하고 있다면 true반환 없으면 false
- .startsWith("문자열") 
: 해당 문자열로 시작하는 문자열인지 true/false
- .endsWith("문자열") 
: 해당 문자열로 끝나는 문자인지 true/false
- .trim() 
: 좌우 공백 제거
- .toUpperCase(), toLowerCase() 
: 대소문자 바꾸기
- .substr(number 시작인덱스,number 길이);
: 시작 인덱스부터 길이만큼의 문자열 반환
- substring(number 시작인덱스, number 끝인덱스);
: 시작 인덱스부터 끝 인덱스까지의 문자열 반환
- .slice(number 시작, number 끝)
: substring()과 동일

<br/>

# ◆ 자바스크립트의 배열
자바스크립트의 배열은 자바의 배열과는 약간의 차이가 있다.<br/>
( 자바의 List컬렉션에 가까운 객체 )
<br/>

#### ▶ 배열객체의 생성
{% highlight ruby %}
var ar = new Array();
var br = [];
var cr = [ 1, -4, 56, 4 ];
var dr = [ true, "스트링", 3 ];
{% endhighlight %}

<br/>

#### ▶ 배열객체 특징
- 자바와 다르게 중괄호({}) 안에서 초기화 하는 것이 아니라 대괄호([]) 안에서 초기화한다.

- 자바의 컬렉션과 비슷하게 <font color="orange">여러 데이터타입을 한 배열 안에 저장</font>할 수 있다.

- <font color="orange">배열에 없는 인덱스(배열 길이 이상의)에도 값을 넣을 수 있고</font>, 중간이 비어 버리게 되면 중간 인덱스들은 undefined 처리하게 된다.<br/>
typeof 빈 인덱스 -> "undefined"를 반환

- 따라서 배열에 데이터 추가 작업은 ar[ar.length] = "데이터"; 형식으로 할 수 있다.

<br/>

#### ▶ 배열객체의 메서드

<br/>

##### ▶ 원본이 바뀌지 않는 메서드
- .concat(배열객체) 
: 두개의 배열 객체를 합쳐서 새로운 배열 객체를 만든다.
- indexOf(내용), lastIndexOf(내용) 
: 내용에 해당하는 인덱스를 반환
- .slice(number start, number end) 
: start부터 end-1 까지 일부 배열을 추출<br/>
( 원본이 바뀌지 않고, end생략 시 끝까지 추출함 )

<br/>

##### ▶ 원본이 바뀌는 메서드
- .sort() 
: 배열을 정렬 시킨다.
- .reverse() 
: 배열을 역순으로 정렬 시킨다.
- .push("내용") 
: 맨 뒤에 요소 하나를 추가하는 메서드  - 길이를 반환
- .unshift("내용") 
: 맨 앞에 요소 하나를 추가하는 메서드 – 길이를 반환
- .pop() 
: 맨 뒤의 요소 하나를 삭제 - 삭제된 요소를 반환
- .shift() 
: 맨 앞의 요소 하나를 삭제 - 삭제된 요소를 반환
- .splice(index, howmany remove, add item ......);
: index부터 howmany 만큼 배열 요소를 지우고 해당 index부터 add item을 추가<br/>
( 뒤에 있는 요소들은 뒤로 밀려난다. )<br/>
{% highlight ruby %}
// 중간 삭제/삽입
ar.splice(3,1,"A","B"); 
=> ar배열의 3번인덱스부터 하나의 요소를 지우고 3번인덱스부터 "A","B" push
// 중간 삽입
ar.splice(4,0,"C");
=> 4번인덱스부터 0개의요소를 지우고 (지우지 않음) 4번 인덱스에 "C"를 push
// 중간 삭제
ar.splice(2,2);
=> 2번인덱스부터 2개를 삭제 ( 2,3번 인덱스삭제 )
{% endhighlight %}

<br/>

# ◆ 자바스크립트의 Date 객체

<br/>

#### ▶ Date객체 생성
- var d1 = new Date();
: 현재시간 기준으로 생성됨.
- var d2 = new Date(int n); 
: 인자를 ms단위로 70년 기준 얼마나 흐른 시간인지를 알려줌<br/>
Ex) new Date(1000)은 1970년 00시00분01초
- var d3 = new Date("2018-01-09");
: 70년 기준 얼마나 흐른 시간인지를 알려줌 ( 그냥 해당 날짜의 Date객체 )

<br/>

#### ▶ Date객체 메서드
- Date.now();
: JAVA의 System.currentTimeMills()와 기능이 같은 메서드 <br/>
현재 시간을 70년기준 ms단위로 반환
- Date객체.getTime()
: 해당 객체의 시간을 ms값으로 반환
- Date객체.toDateString()
: 해당 객체의 날짜를 시간 없이 날짜만 표기
- Date객체.toTimeString()
: 해당 객체의 시간을 날짜 없이 시, 분, 초만 표기
- Date객체.getFullYear();
: YYYY형태로 년도를 반환 ( getYear() 도 있지만 depreacate(곧 사라질 메서드..)됨 )
- Date객체.getMonth()
: 월이 나옴 ( 0~ 11 ) =>따라서 +1을 해야 진짜 월을 알 수 있다
- Date객체.getDate();
: 일이 나옴
- Date객체.getDay();
: 요일이 나옴 0(일)~6(토)
- Date객체.getHours()
: 시간 반환
- Date객체.Minutes()
: 분 반환
- Date객체.getSeconds()
: 초 반환

<br/>

# ◆ Math 객체
수학적인 작업을 수행하는 객체 ( 객체의 생성은 필요하지 않다. )

<br/>

#### ▶ Math객체 메서드
- .abs(n) 
: 절대 값 반환
- .max( x,y,z... ) 
: 최댓값 반환
- .min( x,y,z... ) 
: 최솟값 반환
- .random() 
: 랜덤 값 반환 ( 자바의 random함수와 같은 방식으로 사용한다. )
- .round(n) 
: 소수점 첫째 자리에서 반올림한 값을 반환 ex ) 3.5 = 3
- .ceil(n) 
: 소수점 첫째 자리에서 올림 한 값을 반환 ex) 3.2 = 4
- .floor(n) 
: 소수점 첫째 자리에서 버림 한 값을 반환 ex ) 3.8 = 3

<br/>

#### ▶ 자바스크립트에는 캐스팅이 없기 때문에 floor(n) 작업을 자주 처리함
( string형태로 되어있는 숫자 형태도 해당 작업이 가능하다. )

<br/>

#### 숫자.toFixed(n) : n만큼 소수점 제한을 걸고 반환
ex ) (11/3).toFixed(0) = 4

<br/>

#### ▶ 자바스크립트에서 랜덤정수 뽑아내기.
{% highlight ruby %}
var rd = 1 + Math.floor(Math.random() * 10);
{% endhighlight %}
=자바에서는 int형으로 데이터를 받아낼 시 자동 캐스팅이 되기 때문에 정수 값이 나오지만, 스크립트에서는 floor()메서드를 이용하여 소수점 자리를 강제로 때 주어야 한다.

<br/>

#### ▶ 자바스크립트에서 몫과 나머지 구하기. 
{% highlight ruby %}
console.log(Math.floor(10 / 3) + ", " + 10 % 3);
{% endhighlight %}
=> 몫을 계산할 때의 10/3은 몫이 아닌 실수가 나오기 때문에 소수점 뒷자리는 버려 줘야한다.

<br/>

# ◆ 스크립트의 객체 만들기
스크립트에서는 JSON과 동일한 형태로 객체를 만들 수 있다.
{% highlight ruby %} 
var obj = {
name : "뚜루우",
age : 21,
hobby : [ "게임하기", "게임보기", "게임듣기" ]
};
console.log(obj.name);
{% endhighlight %}
=> 객체설계<br/>
( 마지막 인자는 컴마를 찍지 않는다. ) <br/>
객체 중괄호 마지막은 세미콜론





<br/>