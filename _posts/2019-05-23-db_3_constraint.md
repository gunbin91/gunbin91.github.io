---
layout: post
title: "3. 제약조건(Constraint)"
tags: [ db, constraint ]
date: 2019-05-23
categories: [ db ]
---

<p align="center">
    테이블을 생성할 때 여러가지 제한사항을 둘 수 있다. 제약조건을 거는 방법에 대해 알아보자.
</p><br/>

# ◆ 제약조건(Constraint)
테이블 생성 시 설정할 수 있는 옵션 - 제약조건을 설정할 수 있음.
<br/>

#### ▶ not null 
해당 컬럼 값에 null 값을 허용하지 않음.
<br/>따라서 해당 컬럼에 null값을 넣거나, 미 입력할 시 오류
{% highlight ruby %}
name varchar2(12) not null,
{% endhighlight %}

<br/>

#### ▶ default 
데이터 삽입 시에 입력하지 않은 값들에 대한 디폴트 값 설정
{% highlight ruby %}
gender number(1) default '1',
{% endhighlight %}
=> gender 컬럼 미 입력 시 1이 자동으로 삽입( 단, null값을 입력할 시에는 null이 삽입됨 )

<br/>

#### ▶ constraint 
컬럼에 대한 제약조건을 따로 설정.<br/>
<font color="orange">constraint 제약조건명 제약조건 (컬럼 또는 제약조건)</font>
( 제약 조건 명은 다른 테이블에 있을 시라도 중복이 불가하다. )

<br/>

# ◆ constraint에서 설정할 수 있는 제약조건

#### ▶ PRIMARY KEY (기본키) 
null불가, 중복 불가 
{% highlight ruby %}
constraint rule_01 primary key (name)
{% endhighlight %}
=> name 을 기본 키로하는 rule_01 제약조건을 설정

<br/>

#### ▶ UNIQUE (유일키) 
null가능, 중복 불가
{% highlight ruby %}
constraint rule_02 unique (report)
{% endhighlight %}
=> report 를 유일키로하는 rule_02 제약조건을 설정

<br/>

#### ▶ FOREIGN KEY (외래키) 
다른 테이블을 참조하기 위한 컬럼, references뒤에는 참조하는 테이블(컬럼)을 적어준다.
{% highlight ruby %}
constraint rule_03 foreign key (gender) references gender(code)
{% endhighlight %}
=> gender를 외래키로 하는 rule_03 제약조건을 설정<br/>

외래키가 참조하는 테이블의 키는 references 테이블(컬럼) 으로 설정한다.<br/>
=> gender값을 삽입하고자 할 때, gender테이블에 code데이터 안에 삽입하고자 하는 gender값과 일치하는 값이 있어야 삽입이 가능하다.

<br/>

#### ▶ CHECK
삽입 전 조건검사
{% highlight ruby %}
constraint rule_04 check (weight > '0' )
{% endhighlight %}
=> weight 삽입 시 0 이상인지 체크하는 rule_04 제약조건을 설정

#### ▶ 예시
{% highlight ruby %}
create table baby(
    name varchar2(12) not null, 
    -- 컬럼 설정 시 필수 항목을 지정할 수 있음 ( name컬럼에 null 값을 넣을 수 없다. )
    gender number(1) default '1',
     -- 컬럼 설정 시 기본 벨류를 설정할 수 있음 ( 입력된 값이 없으면 기본 '1' 으로 설정 )
    weight number(3,2),
    birth date,
    report varchar(300),
    constraint babyrule_01 primary key (name),
    -- name은 null값이 있을 수 없고, 중복 데이터도 허용하지 않는다.
    constraint babyrule_02 unique (report),
    -- report에는 null값은 있을 수 있지만, 중복 데이터는 허용하지 않는다.
    constraint babyrule_03 foreign key (gender) references gender(code),
    -- gender값 삽입 시 gender테이블에 code값이 gender값과 일치하는 값이 있어야 삽입이 가능
    constraint babyrule_04 check (weight > '0' )
    -- weight 값은 양수일때만 삽입 가능하다.
)
{% endhighlight %}






<br/>