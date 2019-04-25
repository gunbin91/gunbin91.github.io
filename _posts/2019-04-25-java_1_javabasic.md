---
layout: post
title: "1. Java 프로그래밍 개요"
tags: [ java ]
date: 2019-04-25
categories: [ java ]
---

<p align="center">
    프로그래밍 언어는 크게 컴파일언어와 인터프리터언어로 나뉘어진다. 
    <br/>프로그래밍의 개요에 대해 알아보자.
</p><br/>

# 프로그래밍언어 
### 1. 컴파일
미리 기계어로 바꿔주고 전달 (도구: 컴파일러)<br/>
-> 속도 빠름, 일부에서만 작동
### 2. 인터프리트
실행되는 과정에서 실시간으로 변환 (도구: 인터프리터)<br/>
-> 속도 느림, 어디에서든 작동
<br/><br/>

# JAVA 언어
1995년 제임스고슬링(games gosling)이라는 사람이 만들었고, 가전제품에 탑재할 수 있는 프로그램을 만들기 위한 목적으로 만들어 졌지만, 성공적이지는 못했음.<br/><br/>

### JAVA 프로세스
java언어 => 컴파일 => 프로그램(반 기계어 상태) => 인터프리트(JVM필요)=> 프로세스실행

- Jdk(java development kit): 개발자 도구(jdk설치 시 자동적으로 jre도 설치된다)
- Jre(java runtime environment): 자바프로그램 실행 도구

▶ Java는 컴파일과 인터프리트가 합쳐진 언어
<br/>

▶ Java는 운영체제에 독립적인 프로그램
<br/>
(즉, 사용자 마다 서로 다른 운영체제에 맞는 JVM만 설치하면 어디서든 실행가능)
<br/>

### 명령프롬프트 확인

* 해당경로에서 cmd 실행 : shift + 우클릭
- cd.. : 상위폴더, 
- cd . : 현재폴더, 
- cd 파일명 : 경로이동
- java -version : 설치된 자바 버전 확인
- java -jar Omok_C.jar : 자바로 만든 .jar 파일을 실행하기 위한 명령어<br/>
( java –jar 파일명.jar )<br/>
> 실제 사용자들은 이런 명령어들로 실행시키기 어렵기 때문에
해당 운영체제에서 바로 실행할 수 있게끔 파일을 보통 같이 제공받고,
사용자 컴퓨터 환경 변수에 JRE_HOME 을 설정을 잡아 두라고 함.

<br/><br/>

# ▶ 환경변수 설정
내 컴퓨터 -> 우클릭 -> 속성 OR window키 + pauseBreak
-> 고급 시스템 설정 -> 환경변수 -> 시스템변수<br/>

1. 새로만들기 ->변수이름: JAVA_HOME / 변수값: JDK설치경로 (ex)c:programfile\java\jdk)<br/>
2. Path변수 편집 -> 변수이름 : JRE_HOME / 변수값 : JRE설치경로
 (ex)c:programfile\java\jdk\bin)
 <br/>
 
> 환경변수 설정을 해두면 어느 경로 에서든 javac.exe, java.exe파일 사용이 가능하다.

<br/><br/>

# ▶ 개발환경 구축 
운영체제에 맞는 JDK 설치 
<br/>
( 어느 환경에서든 자바 언어로 작성한 소스파일을 프로그램화 시킬 수 있음 )
<br/>

#### ▶ 소스파일 => (컴파일러)컴파일 => 프로그램
( 이때 상태는 기계어가 아님 / JVM(자바 가상 머신) 이 이해하는 코드 : <font color="orange">바이트코드 상태</font>)
#### ▶ 프로그램 => (자바 가상 머신(JVM)) => 작동 (기계어)
( JVM이 해당 운영체제에 맞는 기계어로 변환 시켜주기 때문에 어디서든 실행 가능하다. )

# ▶ 소스파일 실행
1. 메모장 등의 편집기를 통해 <font color="orange">코드 작성 -> .java 확장자로 저장</font>
<br/>
2. 명령 프롬프트창(cmd)에서 컴파일 : <font color="orange">javac (옵션) 파일명.java</font>
<br/>
=> 해당 클래스명으로 <font color="hotpink">.class 확장자로 파일이 생성된다.(바이트코드파일)</font> 
<br/>

#### Q. 명령어 자체가 안잡힘
A. 환경설정이 되지 않은 상태이다. 시스템변수에 JAVA_HOME // C:\Program Files\Java\jdk1.8.0_144를 추가해준다. ( bin폴더가 설치된 경로 )
-> Path 라는 변수의 경로 값을 변경: 기존 경로에 ;%JAVA_HOME%\bin; 을 추가

#### Q. 변환 실패
A. 코드상의 문제이다 문제점을 찾아 코드를 수정하자.

3 실행: <font color="orange">java 클래스파일명</font>   // 확장자는 붙이지 않는다.<br/>
▶ cmd창에서 시스템 변수 경로 확인 : echo %변수명%

<br/><br/>

# ▶ IDE(통합개발환경)
실제 프로그램 개발에서는 IDE(통합개발환경=개발툴)을 이용해서 프로그램 제작을 하게 된다.
그 중 여러 가지 종류가 있지만, 아래 두 가지 툴이 가장 많이 사용되고 있음.
<br/>

- Eclipse (무료)
- IntelliJ (유료) 
<br/>
( eclipse 는 zip버전과 설치버전으로 받을 수 있다. )

<br/><br/>

# ▶ 코드 작성
코드는 기본적으로 클래스라는것 내부에 main메서드를 작성하는것을 기본으로 시작된다.<br/>
{% highlight ruby%}
public class Test{
    public static void main(String[] args){
        System.out.println("Hello");
    }
}
{% endhighlight %}

####  ▶ main( String[] args)
String[] args 스트링 배열: 컴파일 후 실행 시 들어오는 옵션 값을 저장하는 스트링 배열(실행 시 인자 값)
<br/>
ex ) java App aa <br/>
=> args[0] 을 출력하면 aa가 나온다. ( 공백으로 배열의 인덱스를 나눈다. )

<br/><br/>

# ▶ 이클립스(Eclipse)
#### 컴파일 (ctrl + s)
이클립스에서는 저장과 동시에 컴파일이 실행된다. 즉 명령프롬프트에서 javac의 명령어를 사용하는 것과 같은 액션을 취하는 것이다.
#### 실행 ( ctrl + f11 ) 또는 녹색run버튼 
마찬가지로 명령프롬프트(cmd)에서 java 클래스명 으로 실행 하는것과 같은 액션이다.

<br/><br/>

# ▶ C계열 vs JAVA
C계열의 언어와 JAVA의 <font color="hotpink">가장 큰 차이점은 GC(가비지 컬렉터)</font>이다.<br/>
#### C 
개발자가 직접 메모리에 접근하여 관리하기 때문에 잘못 관리될 경우 메모리의 누수가 발생할 수 있지만 잘 관리되었을 경우 빠르다.

#### JAVA
개발자가 메모리에 직접적인 접근을 할 수 없으며, JAVA가 알아서 메모리를 관리하고 가비지 컬렉션을 하기 때문에 개발자가 편하지만 이 때문에 프로그램이 무거워 질 수 있다.

<br/>