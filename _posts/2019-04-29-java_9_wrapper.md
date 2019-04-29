---
layout: post
title: "9. Wrapper클래스와 정규식"
tags: [ java, wrapperclass, pattern ]
date: 2019-04-29
categories: [ java ]
---

<p align="center">
    기본 자료형에도 해당 데이터를 담당하는 클래스들이 존재하는데 이를 Wrapper클래스라 한다.<br/> 또한 전화번호 형식등에 이용되는 정규식 패턴에 대해 알아보자.
</p><br/>

# ◆ Wrapper class
기본데이터를 객체화 할 때 사용되는 객체들
<table style="overflow:hidden">
    <tr>
        <th>Wrapper Class</th>
        <td>Boolean</td>
        <td>Byte</td>
        <td>Integer</td>
        <td>Double</td>
        <td>...</td>
    </tr>
    <tr>
        <th>기본 자료형</th>
        <td>boolean</td>
        <td>byte</td>
        <td>int</td>
        <td>dobule</td>
        <td>...</td>
    </tr>
</table>
<br/>

#### ▶ Wrap (Boxing)
기본형 데이터를 객체화 시키는 것.
{% highlight ruby %}
Boolean b = new Boolean(true);
Integer i = new Integer(4);
{% endhighlight %}
<br/>

#### ▶ Un Wrap (Un Boxing)
객체화 된 데이터를 다시 기본형 데이터로 바꾸는 것.
{% highlight ruby %}
boolean bb = b.booleanValue();  
//b는 Boolean객체, booleanValue()는 기본형 데이터로 반환
{% endhighlight %}

<br/>

# ◆ Auto Boxing, Auto UnBoxing
Wrapper 객체와 data간에는 자동적으로 박싱과 언박싱이 일어난다.

#### ▶ Auto Boxing
{% highlight ruby %}
int v = 10;
Integer i = v; // Auto Boxing
int vv = i; // Auto Unboxing
{% endhighlight %}
Integer객체에 바로 int형 데이터를 삽입하여 객체 생성 가능
<br/>

#### ▶ Auto UnBoxing 
{% highlight ruby %}
Integer i1 = Integer.valueOf(25); // Boxing
Integer i2 = 21;
System.out.println(i1 > i2); // Auto UnBoxing => true
{% endhighlight %}
객체 값은 기본적으로 비교할 수 없지만, Wrapper클래스의 객체들은 이런 경우 자동 UnBoxing 되기 때문에 비교가 가능하다.( 계산 또는 대입 시 )

- 자동 Boxing 될 때 사용되는 메서드: valueOf()
> 기본적으로 Wrapper클래스의 Boxing은 new를 이용하지 않기 때문에
특정 범위 내( -127 ~ 128 )의 같은 값들을 가진 Wrapper객체들은 같은 객체가 될 수도 있다.

<br/>

# ◆ 데이터 변환
#### ▶ (Wrapper class명).valueOf(변수);
Wraper 클래스에 해당하는 데이터를 변환 리턴 
{% highlight ruby %}
Integer.valueOf(“3”);  // => 문자열 “3”을 Integer형으로 리턴
{% endhighlight %}
<br/>

#### ▶ (Wrapper class변수).intValue();  
래퍼클래스 변수에 해당하는 데이터를 반환리턴   
{% highlight ruby %}
Integer i = 3;  
i.intValue()  // => 3을 int형으로 리턴
{% endhighlight %}
<br/>

#### ▶ (Wrapper class명).parse(Wrapper class명)(스트링데이터);
스트링 형 데이터를 해당 래퍼클래스의 기본데이터형태로 변환 리턴
{% highlight ruby %}
String s = "123";  
int a = Integer.parseInt(s);
String b = "true";  
boolean b = Boolean.parseBoolean(b);
{% endhighlight %}

- int형 데이터 같은 경우 여러 진법이 있기 때문에 매개변수두개인 경우 뒤에 쓰여 있는 수의 진수로 인식
{% highlight ruby %}
Integer.parseInt("223",16); 
// 16진수 223으로 인식하고 10진수 int형 반환
{% endhighlight %}
- Character형은 parse메서드가 없다!

<br/><br/>

# ◆ 패턴검사 
Pattern객체와 Matcher객체를 이용하여 문자열의 패턴을 체크<br/>
Pattern객체와 Matcher객체는 생성을 new로 하지 않음.<br/>

- <b>1. 정규식 Pattern객체를 생성</b> 
<br/>
ex ) Pattern p = Pattern.compile("니다"); <br/>
compile() 메서드의 인자로는 정규식을 쓴다.

- <b>2. 검사할 문자열을 인자로 하는 Pattern객체의 메서드로 Matcher객체 반환 </b>
<br/>
ex) Matcher m = p.matcher(“무엇을 했습니다”);

- <b>3. Matcher객체의 find메서드로 해당 패턴을 찾기</b>
<br/>
ex) m.fine();

{% highlight ruby %}
Pattern p = Pattern.compile("니다");
Matcher m = p.matcher("머머 했습니다. 하지만 아닙니다. 이게무슨 말입니다?");
int cnt = 0;
while(m.find()) {
    cnt++;
    System.out.println(m.group()); // 찾은 문자열 반환
    System.out.println(m.start()); // 찾은 문자열의 시작인덱스 반환
    System.out.println(m.end()); // 찾은 문자열의 끝인덱스+1 반환
}
 System.out.println("찾은 문자열 갯수: " + cnt); // =>3
 m.reset();  
 // find()메서드는 반복이 끝난 후 초기화 되지 않기 때문에 reset()메서드로 초기화 해주어야한다.
{% endhighlight %}

<br/><br/>

# ◆ 메서드 하나로 정규식 패턴 체크
체크할 문자열.matches(정규식문자열);
<br/>  
위와 같이 matches()메서드로 Matcher 없이 바로 비교도 가능. 
<br/>
단, 찾기가 불가능하고 해당 정규식 패턴에 맞는 문자열인지 boolean반환으로 확인하는 용도로 사용한다. 
{% highlight ru by %}
"정규식검사문자열".matches(“[가-하]*”); // => true
{% endhighlight %}

<br/>

# ◆ 정규식 패턴
#### ▶ 문자 하나씩 체크
  - [abc]
  : a 또는 b 또는 c 인가? 
  - [^abc] 
  : except (a or b or c) = a, b, c 를 제외한 모든 문자열
  - [a-zA-Z] 
  : a through z or A through Z  ( a~z, A~Z : 영어 소문자 대문자 )
  - [a-d[m-p]] 
  : a through d, m through p : a-dm-p ( a~d 또는 d~p)
  - [a-z && [def]] 
  : a~z중 def만 
  - [a-z&&[^bc]] 
  : a~z중 bc를 제외한 a~z
  - [a-z&&[^m-r]] 
  : a~z중 m~r을 제외한 a~z
  
<br/>
=> && 가없으면 기본은 or
<br/>

ex ) [abc]a[otz] 
: 첫 번째 문자가 a b c 중 하나로 시작하고 
가운데 문제가 a인 마지막 문자가 o t z중 하나인 문자열

<br/>
  
#### ▶ 기호로 체크
특정그룹은 기호로 정의해 두었기 때문에 기호로 정규식 체크도 가능하다.

- . 
: any character => 모든
- \\\d 
: digit => [0-9]
- \\\D 
: non-digit => [^0-9]
- \\\s 
: whitespace(공백) => \t, \n, \r 포함
- \\\S 
: non-white => [^\\s]
- \\\w 
: word character ( 모든 문자 ) => [a-zA-Z0-9_] ( 단, 한글 제외 )
- \\\W 
: non-word character
{% highlight ruby %}
System.out.println("1".matches("[\\d]")); //=> true
{% endhighlight %}
- . (닷)등 특수기호(?.*.+)로 쓰이는 문자를 패턴이 아닌 문자자체로 검사하기 위해서는 \\\. \\\? 등으로 표기!
<br/><br/>

#### ▶ Quantifiers ( 수량한정 )
  
- ? 
: 있거나 없거나 true<br/>
ex ) \\\d[s]?  : 숫자 뒤에 s가 있어도 true, 없어도 true

- \* 
: 없거나 많거나 true<br/>
ex ) A\\\d*  :  A뒤에 숫자가 없거나 숫자만 여러 개거나 true

- \+ 
: 하나이상 있으면 true<br/>
ex ) \\\d*[a-z]+  :  숫자 뒤에 소문자가 하나이상 있어야 true

- {n} 
: 반드시 n개가 있어야 true<br/>
ex ) \\\d{2}[가-휳]\\\d{4}
: 반드시 숫자 두개로 시작하고, 사이에 ‘가~휳’ 문자 하나, 끝에는 반드시 숫자 4개 

- x{n,} 
: 최소 n개 이상 있어야 true<br/>
ex ) \\\d{4,} : 반드시 숫자 4개 이상으로 시작

-  x{n,m},  x{n,m}?,  x{n,m}+  
: at least n but not more than m (n~m사이)<br/>
ex ) 01[016789]-\\d{3,4}-\\d{4}  : 핸드폰번호검사

#### ▶ 그룹 패턴
( ) 괄호로 묶여있는 패턴은 여러 개로 검사할 수 있다.
<br/>
ex) ([a-z]{2}\\d)+ 
: 문자2숫자1 패턴이 계속 이어지는지 검사
- 한번 탐색된 그룹에 속한 문자는 다른 그룹에도 속할 수 없다!
- find()후 group() 으로 찾으면 찾은 문자가 나오지만, 정규식을 그룹으로 처리할 시 group(n)으로 처리하면 n번째 그룹만 따로 뽑을 수 있다.





<br/>