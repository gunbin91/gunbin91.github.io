---
layout: post
title: "2. 데이터 연산"
tags: [ java ]
date: 2019-04-25
categories: [ java ]
---

<p align="center">
    자바에서 사용되는 기본 연산 및 문법을 간단하게 알아보자.
</p><br/>

# ◆ 진법 표기법 
자바에서는 숫자 앞에 표기에 따라 진법을 달리 인식한다.
<br/>

 ▶ 10진수 :  그냥 숫자 ex) 15 <br/>
 ▶ 2진수 : 앞에 0b를 붙이다. ex) 0b101 <br/>
 ▶ 8진수 : 앞에 0을 붙인다. ex) 013 <br/>
 ▶ 16진수 : 앞에 0x를 붙인다.  ex) 0x3df <br/>
 => 출력은 모두 10진수

<br/><br/>

# ◆ 쉬프트 연산
▶ << (왼쪽 쉬프트) :  2의 n제곱만큼 곱해진다.  <br/> 
ex) 134 << 2 = 134 x 2^2
<br/>
(실제로 비트를 왼쪽으로 n칸만큼 이동)
<br/>
▶ >> (오른쪽 쉬프트) : 2의 n제곱만큼 나눠짐 
<br/>
ex) 134 >> 7  = 134 / 2^7
<br/>
(실제로 비트를 오른쪽으로 n칸만큼 이동)

<br/><br/>

# ◆ 정수
- 기본 정수들은 4byte(32bit)로 저장할 수 있는 범위이다. ( 기본 int형 )
- 맨 앞의 비트는 부호 비트로 실제 데이터가 아니라 부호 결정용임 ( 0: 양수, 1: 음수)
- 1111_1111_1111_1111_1111_1111_1111_1111은 양의 정수 최대가 아닌 음수
- 4byte의 양의 정수 최댓값: 0111_1111_1111 ...
- 4byte의 음의 정수 최댓값: 1000_0000_0000 ...
cf) 4byte를 채우지 않고 적은 2진수 형태의 값들은 앞에 그만큼의 0이 채워져 있다.
- 100(2) = 8 => 실제로 000000000.....100
- 기본 int형 정수의 범위를 넘는 정수 값을 표기할 때 끝에 L을 붙여서 Long형태로 변환시켜준다. 그렇지 않으면 범위초과 오류 ex) 5000000000000L

<br/><br/>

# ◆ 실수
- <font color="hotpink">기본 실수들은 8byte(double형)</font>으로 저장함
- 실수는 정수와 다르게 정확한 값을 저장하지는 않는다. <br/>
( 최대한 가까운 값으로 저장 / 약간의 오차 발생 ) 
<br/>
=> 자릿수를 높이고 정밀도를 줄인 방식.
- 실수도 마찬가지로 <font color="hotpink">다른 자료형과 계산 시 큰 자료형에 맞춰서 변환 계산됨</font><br/>
ex) 2.0 / 3.0f = double형 8byte로 계산됨

<br/><br/>

# ◆ 논리형 데이터
- 1byte(boolean형), true / false
- 크기 비교와 동등 비교 연산을 할 수 있다.
- && 연산: 두 개의 피 연산자 모두 true일 때 만 true를 반환

ex) true && true = true
- \|\| 연산: 둘 중 하나라도 true면 true를 반환 

ex) true || false = true
- \|\| 보다 &&의 우선순위가 높다. 단, &&보단 괄호의 우선순위가 더 높음.

<br/><br/>

# ◆ 문자/문자열 데이터
- 문자 데이터(char): 2byte
- 문자열 데이터(String): 2byte * 문자 수(문자들의 배열)
<br/>
=> java에서 <font color="hotpink">char형은 작은 따옴표(‘’)로 표시하고, 문자열은 큰 따옴표(“”)로 표기</font>한다.
- 문자열의 +연산: 문자열 합치기 
ex) "문자" + "들" = "문자들"
- 문자열 + 정수 = 문자열 합치기 
ex) "문자"+1+2+3 = 문자 123
<br/>
=> 문자열 옆에 정수를 계산하기 위해서는 괄호 안에서 계산 후 더해야 한다.
- 유니코드 값을 이용하여 문자를 출력 할 때는 '\u'를 앞에 붙인다.
ex) '\uc790' 을 출력하면 '자' 가 출력됨

#### ▶ 특수 문자 표기법 
쌍 따옴표: \\", 역 슬러시 : \\\, 홑 따옴표 : \\',  라인 띄기 : \\n,  탭(tab) : \\t

<br/><br/>

# ◆ 자료형
1byte = 8bit / 1bit는 0과1을 표현할 수 있으므로 표현범위는 2^비트 제곱
- 1byte: boolean(논리데이터), byte(정수형) => 정수범위 127(2^7 - 1) ~ -128(-2^7)
- 2byte: short(정수형), char(문자형) => 정수범위 32767(2^15 -1) ~ - 32768(2^15)
- 4byte: int(정수형), float(실수형)
- 8byte: double(실수형), long(정수형)
- 기타: String형

<br/><br/>

# ◆ 객체자료형
객체자료형은 4byte의크기를가지며, <font color="hotpink">객체자료형으로 선언한 변수는 실제로 객체를 저장하는 것이 아닌 해당 객체의 주소값(레퍼런스값)을 가지는 역할</font>을 한다. ( C에서의 포인터와 같음 )

> String또한 객체로서, String도 객체자료형으로 동작된다.

<br/><br/>

# ◆ 변수 사용 시 주의점
1. 데이터의 종류와 다른 값을 저장 할 수 없다. ex) int n = 3.14 (x)
2. 중복된 변수명 ex) int n; float n; (x)
3. 예약어 ex) int void; (x)
4. 공백 포함 ex) int a b; (x)
5. 숫자로 시작 ex) int 1f; (x)
6. 자바는 대소문자를 구분한다. ex) int n; int N; (o)
7. 변수명을 작성할 때는 용도에 맞게 작명 하는 것이 좋다. ( 코드를 쉽게 파악할 수 있게 )
ex)  이름,성별 등의 변수명은 String name, gender 등의 형식으로..
8. <font color="hotpink">camel naming rule</font> : 일반적인 작명룰 (코드 상의 오류는 아니지만 지켜야할 규칙)
<br/>
=> 변수의 <font color="orange">첫 문자는 소문자로 작명 / 두 단어 이상이 합쳐진 형태의 변수명은 두 번째 단어부터 첫 문자를 대문자로 작명</font>
<br/>
ex ) long stockPrice
9. 변수명에 언더바( _ )를 사용할 수 도 있는데, <font color="orange">보통 final값(상수)을 가지는 변수를 선언할 때 언더바를 사용하고, final값은 룰에 따라 대문자( UpperCase )로 표기</font>한다.
<br/>
ex ) final TOTAL_COUNT = 100;

<br/><br/>

# ◆ i += 1 과 i = i+1 의 차이
▶ i += 1 은 계산 후 자동으로 i의 데이터 자료형에 맞게 변환되어 저장되고,
<br/>

▶ i = i+1 은 계산결과가 i의 데이터 자료형과 일치하지 않는 경우 오류가 발생한다.<br/>
ex ) int i=1;  <br/>

> i+=2.0  가능 => double형으로 3.0 계산 후 int형으로 변환되어 저장됨. ( 자동 캐스팅 )<br/><br/>
i = i+2.0  불가능 => double형으로 계산되어 int형 변수에 저장불가 ( 수동 캐스팅(명시적 형 변환) 필요 )

<br/><br/>

# ◆ Cpu에서 처리되는 명령어(또는 순서) 확인 
.class파일이 있는 위치에서 CMD실행 후 javap –v ~.class<br/>
=> load, store.. 등의 순서를 확인 할 수 있다.

<br/><br/>

# ◆ 연산자 우선순위
#### 1. 단항 연산자( ++, -- ....)
#### 2. 이항 연산자 ( +, -, >> ...)
#### 3. 삼항 연산자 ( +=, -= ...)

<br/><br/>

# ◆ e를 이용한 실수표기 방법
- 2000 을 e를 이용하여 표기
<br/>2e3 또는 2e+3 => 2 * 10^3<br/>
- 0.002 를 e를 이용하여 표기
<br/>2e-3=> 2 * 10^-3
<br/>
=>  숫자 오른쪽의 e는 *10을 의미하고, e의 오른쪽의 숫자는 10의 n거듭제곱을 의미

<br/><br/>

# ◆ println과 printf의 차이
<font color="orange">println() 메서드는 마지막 부분에 개행을 포함하여 자동으로 개행</font> 되고, printf는 개행을 포함하지 않는다.
또한 <font color="hotpink">printf는 %s, %d등의 서식 문자를 사용할 수 있지만</font>, println에서는 서식문자사용이 불가능하다.

<br/><br/>

# ◆ 서식문자
#### 정수 서식 문자
- %d: 10진수
- %o: 8진수
- %x: 16진수

#### 문자 서식 문자
- %c: char형 문자
- %s: String형 문자열

#### 실수 서식 문자
- %f: 실수형

#### 특수 서식 문자 사용법
- %5d: 정수형 서식 문자 앞에 숫자를 표기하면 해당 수 만큼 공백을 두고 오른쪽 정렬시킨다.<br/>
Ex ) %5d로 1234를표기 ->      1234

- %5f: 실수형 서식 문자 앞에 숫자를 표기하면 소수점 이하 자리 수를 정할 수 있다.<br/>
Ex ) %5f로 0.12345678을표기 -> 0.12345

<br/><br/>

# ◆ 조건연산자(삼항연산자)
조건식? 식1:식2
으로 사용하는 연산자로, 조건식이 true면 식1의 값이 반환되고, false면 식2의 값이 반환된다.
{%highlight ruby%}
int result = 10>20? 50:100;
{%endhighlight%}
=> 조건식이 참이면 result값은 50이되고, 거짓이면 100이된다.

<br/><br/>

# ◆ 조건문
#### if~else 문
{%highlight ruby%}
If(조건식){
    System.out.println("if참");
}else if(조건식){
    System.out.println("else if참");
}else{
    System.out.println("참이없음");
}
{%endhighlight%}
조건식이 참일 때 만 작동되는 구문, else는 조건식이 false일 때 작동된다.

<br/>

#### switch문
{%highlight ruby%}
switch(a){
case 10:
    System.out.println("a는10입니다.");
    break;
case 20:
    System.out.println("a는20입니다.");
    break;
default:
    System.out.println("a는10과20이 아니다.");
    break;
}
{%endhighlight%}
Switch문 안의 변수 값이 case값과 일치하는 구문만 실행되고 일치되는 case값이 없을 경우 default문이 실행됨.<br/>
주의 해야 할 점은 case문이 실행되고 해당 case문의 아래배치되는 모든 case가 실행되기 때문에 <font color="orange">case문이 끝나는 지점마다 break; 키워드를 붙여주어야 한다.</font>

<br/><br/>

# ◆ 반복문
#### for문
{%highlight ruby%}
for(int i=0; i<10; i++){
	System.out.println("i의 값은"+i+"입니다.);
}
{%endhighlight%}
for문의 구성은 (변수값 초기화; 조건식; 증감문)으로 조건식이 false가 되기 전까지 반복한다

<br/>

#### while문
{%highlight ruby%}
while(i<10){
	System.out.println("i의 값은"+i+"입니다.);
}
{%endhighlight%}
while문은 조건식만 존재함으로, 변수값의 초기화나 증감문은 필요시 따로 처리를 해 주어야 한다.

<br/>

#### do~while문
{%highlight ruby%}
do while(i<10){
	System.out.println("i의 값은"+i+"입니다.);
}
{%endhighlight%}
Do~while문은 조건에 관계없이 무조건 첫번째 한번은 실행되고, 그 이후에는 while문과 똑 같은 동작 구조를 가진다.


<br/>