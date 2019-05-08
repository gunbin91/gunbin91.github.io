---
layout: post
title: "17. JAVA API"
tags: [ java, java api ]
date: 2019-05-08
categories: [ java ]
---

<p align="center">
    자바에서는 주로 많이 쓰이는 기능들에 대해 미리 구현된 클래스의 함수들이 있다.<br/>
    자주 쓰이는 api들에 대해서 알아보자.
</p><br/>

# ◆ API ( Application Programming Interface )
운영 체제나 프로그래밍 언어가 제공하는 기능을 제어할 수 있게 만든 인터페이스로서, 라이브러리처럼 다운받아 쓰지 않고, 기본적으로 제공되는 기능

<br/>

# ◆ Math 클래스 
수학적 연산을 다루는 클래스.

#### ▶ Math클래스 메서드
- Math.random()  
: 0.0 <= x < 1.0 사이의 랜덤 double 값 반환 하는 메서드.<br/>
=> <font color="orange">(int)(Math.random() * N)</font> : 0 <=~< N-1 사이의 정수<br/>
=> S + (int)(Math.random() * N) : 0+S <=~< N+S 사이의 정수<br/>

- Math.sqrt(n) 
: 루트값 계산
- Math.pow(a,b) 
: a의 b제곱을 구해주는 메서드.
- &nbsp;<font color="hotpink">Math.max(n1, n2)</font> 
: n1,n2 중 큰 값을 반환
- Math.abs(n) 
: n의 절대 값을 계산해줌.

<br/>

# ◆ String 클래스 
문자열관리 클래스
#### ▶ String클래스 메서드
- new String (char[] , int , int)
: 인자가 3개인 생성자 char배열의 (int)인덱스 ~ (int)개수까지를 String형 객체로 생성
- &nbsp;<font color="hotpink">String형데이터.indexOf(String);</font>
: 인자인 해당 String문자열을 앞에서부터 맨 처음 찾은 인덱스 위치 int반환<br/>
(인자가 두 개인 경우 두 번째는 int형, => 해당 인덱스부터 찾기 )
- String형데이터.lastindexOf(String);
: indexOf()를 맨 끝 인덱스부터 찾는 메서드.
- &nbsp;<font color="hotpink">String형데이터.contains(String);</font>
: 해당문자열이 있는지 boolean리턴
- String s = Integer.toString(n, o); 
: n을 o진수 String형으로 변환하는 메서드. ( n,o은 int형 )
- String변수.charAt(인덱스번호)  
: 문자열에서 해당 인덱스에 해당하는 문자를 char형으로 반환
- String.format();    
: c언어의 printf와 같은 형식이 있는 문자열을 반환할 수 있음<br/>
ex ) String.format("머머 : %d ",  i );
- char[] ar = String데이터.toCharArray();  
: 문자열을 캐릭터형 문자배열로 반환
- String변수.intern(); 
: 해당 String객체와 같은 상태의 char[]상태인 객체를 String pool에서 뽑아내는 메서드
> new로 생성한 스트링 객체는 같은 문자열을 가지고 있더라도 다른 객체지만,
intern()으로 뽑아낸 문자열이 같을 경우 같은 (주소)값을 가짐
<br/>
( String객체는 특별히 new를 사용하지 않더라도 문자열만으로 객체를 생성할 수 있지만 그렇게 생성된 문자열객체는 String pool이란 특별한 곳에 저장되기 때문에 문자열이 같으면 같은 객체 값을 가진다. 따라서 intern을 이용하여 뽑아낸 문자열과 같다면 같은 객체 값을 가짐.)
<br/>
=> <font color="orange">String값을 비교할 때는 .equals()를 사용</font>하지만 문자열이 긴 경우 intern()을 이용하여 비교하면 빠른 처리가 가능하다!!

- &nbsp;<font color="hotpink">String형변수.split(문자열);</font>
: 매개변수로 받은 문자열을 기준으로 문자열을 쪼개서 String[]형 배열로 리턴.<br/>
( 매개변수로 받은 문자열은 포함하지 않은 배열이 리턴 된다. )<br/>

> split(문자열, n) : n개 이상일 때는 그 미만만 분리하고 나머지는 하나로 묶음<br/> <font color="orange">split의 매개인자 문자열은 정규식으로 사용</font>하기 때문에 "." 으로 분리할 때는 \\. 으로 적어준다.

- &nbsp;<font color="hotpink">.toUpperCase()</font>  
:  문자열을 대문자로 변경 리턴
- &nbsp;<font color="hotpink">.toLowerCase() </font>
:  문자열을 소문자로 변경 리턴
     
- .replace(문자열,문자열); 
: 호출한 문자열의 첫 번째 매개변수 문자열을 두 번째 매개변수 문자열로 변환 리턴
- .startsWith(문자열)  
: 해당 문자열로 시작하는 문자열인가를 boolean리턴
- .endsWith(문자열)  
: 해당 문자열로 끝나는 문자열인가를 boolean리턴
- .matches(정규식);
: 해당 문자열이 정규식과 일치하는지 검사 boolean리턴
- .substring(n),  or substring(n,m)
: 인덱스 n부터 문자열반환.. n~m까지 반환
- String.copyValueOf(char[] a);  
: 인자 char배열을 String형으로 반환

<br/>

# ◆ StringBuilder 클래스 
문자열 변경 등의 작업을 하는 클래스.<br/>
=> String클래스와 차이점 : 문자열의 수정이 가능하다.

#### ▶ StringBuilder클래스 메서드
- .insert(n,문자열(아무데이터)) 
: 인덱스번호 n에 문자열을 삽입
- .append(문자열) 
: 문자열 끝에 괄호 안 문자열을 더하기.<br/>
=> String클래스에서 += 하는 것과 같은 기능을 하지만 스트링 객체는 계속 생성되기 때문에 append()를 사용하는 것이 메모리관리에 효율적!!
- delete(int,int)  
: 인덱스이상 인덱스미만 까지 삭제
- deleteCharAt(n) 
: n번 인덱스삭제
- replace(int, int, String)
: 인덱스~ 인덱스를 다른 문자열로 대체
- setCharAt(int, char)
: 인덱스를 다른 문자로 대체
- reverse()
: 문자열뒤집기
<br/>
- StringBuilder객체는 String객체는 아니기 때문에 equals로 스트링과 비교가 불가능하다.<br/>
=> .toString으로 String으로 변환 후 비교가능!

<br/>

# ◆ Point 클래스 
좌표 관리 클래스.
<br/>

#### ▶ Point클래스 메서드
- new Point(x,y) 
: x,y의 좌표를 가진 객체를 생성.
- .translate(x,y) 
: 해당객체의 좌표를 x,y만큼 이동
- .move(x,y) 
: 해당객체의 좌표를 x,y로 변경

<br/>

# ◆ Rectangle 클래스 
사각형 데이터 처리 클래스
<br/>

#### ▶ Rectangle클래스 메서드
- new Rectangle(10,40,70,80)  
: (x,y) 좌표상의 70x80 사각형 ( 좌표는 밑으로 커짐 )
- .getMaxX() 
: 최대 x값=> x + width
- .contains(15, 45) 
: 해당 좌표가 만들어진 객체 좌표 안에 포함(교차영역)되어 있는지 검사.
- intersects(r2) 
: 객체를 통째로 넘겨주는 메서드로 괄호안의 객체가 호출한 객체 안에 포함되는지 검사

<br/>

# ◆ Date 클래스 
흐른 시간을 다루는 클래스
<br/>

#### ▶ Date클래스 메서드
- &nbsp;<font color="hotpink">.getTime()</font> 
: 아무 설정 없이 출력했을때 <font color="orange">System.currentTimeMillis()</font>와 같은 70년대~현재까지의 시간을 ms(long타입)로 반환
- setYear(n), setMonth(n) 
: 등의 메서드로 현재시간설정 등을 통해서 설정한 시간부터 현재까지의 시간을 구할 수 있다.
- Date 변수의 객체를 그냥 출력할 경우 현재 날짜가 나옴. ( toString() 호출 )

<br/>

# ◆ Integer 클래스 
int형 데이터를 객체로 다루는 클래스
<br/>

#### ▶ Integer클래스 메서드
- &nbsp;<font color="hotpink">Integer.parseInt(문자열, n) </font>
:  해당 문자열을 n진수로 인식 후 10진수 int형변환 ( n이 없을 시10진수 )
- &nbsp;<font color="hotpink">Integer.toString(n)</font> 
: int형 n을 String형으로 변환

<br/>

# ◆ Number 클래스 
Integer, Double, Long ... 숫자관리 클래스들의 부모클래스<br/>
=> 추상클래스이기 때문에 객체 생성 불가.

- intValue() 
: 숫자를 int형으로 변환해주는 메서드<br/>
=> DoubleValue(), FloateValue() .... 등등

<br/>

# ◆ Arrays 클래스 
배열객체를 편하게 다루기 위한 클래스.
<br/>

#### ▶ Arrays클래스 메서드
- Arrays.toStriong(배열변수); 
: 배열의 내용을 출력 ( 0~ length-1 까지)<br/>
=> Arrays클래스 내부에서 각각의 데이터 형에 대한 오버로드가 되어있음.
- Arrays.sort(배열)  
: 정렬

<br/>

# ◆ Scanner 클래스  
콘솔입력을 받기위한 클래스
<br/>

#### ▶ Scanner클래스 메서드
- Scanner scan = new Scanner(System.in);   
: 객체 생성
- scan.nextInt();  
: int형 데이터를 입력받기위한 메서드.

<br/>

# ◆ Console클래스
콘솔창의 입력 제어
<br/>

#### ▶ Console클래스 메서드
- Console console = System.console();  
: 콘솔객체 생성  
- console.readLine("account id> ");  
: 스트링읽기 ( 인자의 문자열은 메시지 )
- console.readPassword("account pass> ");
: 안 보이는 스트링(또는 char[])읽기
- ctrl + c 
: 콘솔 빠져나가기!

<br/>

# ◆ 기타 API
- JOptionPane.showMessageDialog(null, 문자열);
: 다이얼로그 창으로 표시. (팝업)
- int a = JOptionPane.showConfirmDialog(null, "Do you want to Exit?");
: 다이얼로그 창 (예(0), 아니오(1), 취소(2)) int형 반환 
- System.identityHashCode(n)
: n의 JVM상의 위치를 int형으로 반환해주는 메서드<br/>
(n은 상수,변수,객체 등등이 올 수 있다.)
- System.exit(0)  
: 강종
- &nbsp;<font color="hotpink">System.currentTimeMillis() </font>
: 1970.01.01  00:00:00 부터 지금까지 흘러간 시간을 long형으로 반환
- Thread.sleep(1000); 
: 강제지연 (단위 ms)

<br/>

- 클래스 소스 보기 
: 클래스 Ctrl + 좌 클릭 -> 경로설정을 jdk-> src.zip을 잡아주면댐
- 클래스 정보보기 
: java.oracle.com > java download > java APIS > java 8 
- 상속정보
: 클래스 좌 클릭 -> f4
- &nbsp;<font color="orange">java.lang소속의 클래스들은 import를 하지 않아도 사용 가능</font>하다.










<br/>