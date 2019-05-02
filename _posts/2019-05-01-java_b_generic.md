---
layout: post
title: "11. 제네릭(Generic)"
tags: [ java, generic ]
date: 2019-05-01
categories: [ java ]
---

<p align="center">
    앞서 컬렉션을 사용할 때 <>안에 타입을 미리 지정해 주었는데 이것을 제네릭이라 한다. 자세히 알아보도록 하자.
</p><br/>

# ◆ 제너릭(Generic)
객체 설계 시 객체를 생성할 때 타입을 지정할 수 있도록 해주는 기능

<br/>

#### ▶ 제너릭 설정방법
객체 설계 시 <font color="orange">클래스명 뒤에 &lt;E&gt;등의 형태를 지정</font>해주고, 이 E를 클래스명 대신 사용하면 된다.<br/>
<>안에 쓸 수 있는 문자는 E(Element), T(Type), K(Key), V(Value) 등이 있고, 어느 것을 사용해도 상관은 없으나, 각각 의미에 맞게 사용해 주는 것이 좋다.

<br/>

#### ▶ 제너릭을 이용한 클래스 설계 예시
{% highlight ruby %}
class Sample<E>{
    E data;
    E currnetData(){ return data; }
    void changeData(E data) { this.data = data; }
}
{% endhighlight %}

<br/> 

#### ▶ 제네릭 제한걸기
제네릭을 사용할 때 <E extends 클래스>로 사용하게 되면, 해당 상속된 클래스 계열의 객체들만 제네릭 값으로 받을 수 있다. 또한 제네릭 값을 받아오지 않을 시 디폴트 타입인 Object로 설정된다.

- ex ) class Tester&lt;T extends Number&gt;{  }
: 디폴트 설정 값은 Number이 되고, 제네릭 값으로 받을 수 있는 것은 Number계열(상속)인 Integer, Double... 등만 가능하다

<br/>

#### ▶ 제너릭객체 생성
- Sample p = new Sample(); 
:  제네릭 데이터 미 설정시 디폴트인 오브젝트로 설정됨!<br/>
( 오브젝트 형을 사용하더라도 명시해 주는 것이 좋다. )

- 제너릭은 클래스형태만 지정할 수 있고, int, float같은 기본형 데이터는 지정할 수 없다.
<br/>=> int[]는 배열 객체이기 때문에 가능.

- 이를 통해 컬렉션 객체들이 제네릭을 이용하여 설계 되었다는 것을 알 수 있다.







<br/>