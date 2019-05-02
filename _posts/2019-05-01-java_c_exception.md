---
layout: post
title: "12. 예외처리"
tags: [ java, javaerror, exception, trycatch ]
date: 2019-05-01
categories: [ java ]
---

<p align="center">
    예외란 프로그램이 비정상적으로 종료될 수 있는 코드지점을 말한다. <br/>이를 처리하는 방법에 대해 알아보자.
</p><br/>

# ◆ Throwble 
JVM의 비정상 종료를 유발시키는 특수 객체로 Error과 Exception객체들의 최상위 클래스이다.<br/>
Throwble은 두 계열의 클래스들이 존재한다. ( Exception / Error )

#### ▶ Error  
Throwble의 두 계열 중 하나로, <font color="hotpink">하드웨어적인 결함</font> 때문에 발생하는 예외에 대한 객체다. 따라서 <font color="hotpink">개발자가 대처할 수 없는 문제</font>들이다.
- StackOverFlowError
: 해야 할 작업이 밀리는 경우에 생김 ( Cpu사양 문제 ) 
- OutOfMemoryError
: 허용 메모리가 초과되는 경우에 발생 ( Ram사양 문제 )

<br/>

#### ▶ Exception 
Throwble의 두 계열 중 하나로 <font color="hotpink">프로그램상의 문제</font>로 발생하는 것들이다 따라서 <font color="hotpink">개발자가 대처할 수 있다</font>.

<br/><br/>

# ◆ 예외 처리

#### ▶ throw 키워드 
Throwable 계열의 객체들만 사용할 수 있는 <font color="orange">에러및 예외를 강제로 발생시키는 키워드</font>로,
throw를 앞에 붙이고 Throwble계열의 객체를 생성시키면 해당 지점에서 해당 객체가 강제로 발생된다.
{% highlight ruby %}
throw new RuntimeException(); //강제적으로 익셉션 오류 발생!
{% endhighlight %}

<br/>

#### ▶ try ~ catch ( 예외 처리 )
Exception이나 Error가 발생하여 강제종료 될 수 있는 코드에 <font color="orange">종료시키지 않고 catch하여 다시 다른 코드들의 흐름이 계속 진행</font>될 수 있도록 유도해주는 처리<br/>
try문 내부의 예외 발생 지점 이후의 코드는 실행되지 않는다.
{% highlight ruby %}
try{ 
    int n = Integer.parseInt("1a",10); 
}catch( NumberFormatException e ){
    e.printStackTrace();
    System.out.println(e.getMessage); 
}
{% endhighlight %}
catch의 매개변수로 들어오는 객체와 일치하는 비정상 종료(예외)가 발생했을 시, 종료하지 않고 catch문을 처리한 후 다음 코드로 계속해서 진행할 수 있게 해준다.<br/>

단, 해당 매개인자와 다른 예외는 잡아낼 수 없고 비정상 종료된다. 
따라서 <font color="orange">모든 비정상 종료를 막고 싶을 때는 catch(Throwble e)로 처리</font>하면 된다.<br/>
( 모든 예외는 catch(Exception e) )

<br/>

#### ▶ catch문의 매개인자 메서드
- e.getMessage 
: 해당 예외에 대한 간단한 정보를 String으로 반환
- e.printStackTrace() 
: 해당 예외에 대한 모든 정보를 콘솔창에 출력해주는 메서드.

<br/>

#### ▶ 반드시 예외처리를 해야하는 Throwable
Throwble중에는 예외 처리를 하지 않으면 컴파일이 되지 않아 반드시 예외처리를 해야 하는 Throwble객체들이 있다. Error계열은 예외처리를 꼭 할 필요는 없고, Exception계열 중 일부는 반드시 예외처리를 해야 하는 객체들이 있다.
<br/>

- Checked Exception 
: try~catch를 꼭 해야 함 ( 하지 않으면 컴파일이 실패 )
<br/>=> 파일처리, 네트워크처리등
- UnChecked Exception 
: try~catch가 필수는 아님 ( 컴파일은 되지만 예외 발생시 터짐 )
<br/>=> 데이터 오류등

<br/>

#### ▶ 멀티 catch / 동시처리
- try{}catch(){}catch(){} 의 형식으로 여러 예외상황을 처리할 수 있다.
- catch(IOException \| IllegalArgumentException e) 의 형식으로 동시에 처리도 가능하다.(변수는 하나만)

<br/>

#### ▶ finally
try{} catch(){}  finally{} 형식으로 쓰는 <font color="orange">finally는 catch에서 잡히던 안 잡히던 무조건 실행되는 구문</font>이다.<br/>
즉 catch문 밖에 그냥 작성한 것은 cath로 잡지 못한 다른 예외가 발생한 상황에서는 진행되지 않지만, finally 문에 작성한 코드는 무조건 실행된다.

<br/><br/>

# ◆ Exception 상속구조
상위 Exception클래스로 예외 처리(try ~ catch)할 시 하위Exception의 예외 상황을 모두 잡아 낼 수 있다.<br/>
>ex) StringIndexOutOfBoundsException 과 ArrayIndexOutOfBoundsException 는
IndexOutOfBoundsException의 하위 Exception이기 때문에 상위 클래스하나로 두개의 예외 상황을 모두 잡아낼 수 있다.

- catch문에 상위클래스를 먼저 작성할 시, 밑에서 하위클래스로 catch하는 것은 불가능하다.<br/> ( 어차피 상위클래스에서 모두 잡아내기 때문에 )단, 그 반대의 경우는 가능하다.

- 최상위 Exception 으로 catch할 시 장/단점 
: 장점은 모든 Exception을 다 잡아낼 수 있다는 것이고, 단점으로는 상황별 처리가 불가능하다.
<br/>
따라서 먼저 특수하게 처리해야 할 Exception계열의 하위클래스들을 처리하고,
밑에 최상위 Exception을 써주는 형태가 가장 많이 쓰이는 형태
{% highlight ruby %}
try {
} catch (IllegalArgumentException e) {  // IllegalArgumentException 만 잡아냄
} catch (Exception e) { // 모든 Exception 계열을 다 잡아낼 수 있음.
} catch (Error e) { // 모든 Error 계열을 다 잡아낼 수 있음
} catch (Throwable e) { // 모든 Exception / Error 계열을 다 잡아낼 수 있음.
}
{% endhighlight %}

<br/>

# ◆ 예외 전가( throws )
익셉션을 꼭 직접 예외처리(try ~ catch)해야 되는 것은 아니고, 이 <font color="orange">작업을 호출한 곳으로 넘겨서 그쪽에서 처리</font>를 시킬 수 있음.
<br/>

- 메서드 뒤에 throws 키워드를 붙이고 처리해야하는 Exception 클래스명을 써준다.
{% highlight ruby %}
public static void main(String[] args) throws InterruptedException
{% endhighlight %}
=> 이렇게 하면 try~catch없이 Checked Exception을 처리할 수 있다.
<br/>

>주의) main메서드에 붙여두는 것은 좋은 방법은 아니다. <br/>
=> main에서는 다른 곳으로 넘기는 것이 불가능하기 때문에 JVM에게 넘기게 되는데 예외가 발생하면 터져 버림<br/>







<br/>