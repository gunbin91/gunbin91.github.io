---
layout: post
title: "19. 일괄처리(Batch Processing)"
tags: [ spring, spring batch ]
date: 2019-11-05
categories: [ spring ]
---

<p align="center">
    
</p><br/>

## ◆ 일괄 처리(batch processing)
개별적으로 특정 요청에 따라 처리되는 것이 아닌, 한꺼번에 일괄적으로 대량 건을 처리하는것을 일괄처리(Batch)라고 한다.<br/>
또한 배치는 보통 정해진 특정한 시간에 실행되므로 <font color="orange">업무의 효율성과 비효율적인 시스템의 과부하를 줄이기 위해 사용</font>된다.

#### 특징
- 1 <font color="orange">대량의 데이타</font>를 처리
- 2 <font color="orange">특정 시간</font>에 실행 
- 3 <font color="orange">일괄적</font>으로 처리

<br/>

## ◆ Spring3 스케쥴러(Scheduler) 사용법
스케쥴러란 특정 시간에 해야할 작업은 할당하는 역할을 한다.<br/>
Spring3이상에서는 @Scheduled 어노테이션을 통해 특정 시간에 특정 메서드를 호출시킬 수 있다.

<br/>

### ▶ 스케쥴러등록

#### 1. Spring bean configuration.xml 설정
스케쥴러 사용을 위해 &lt;beans>태그의 아래 속성을 추가해준다.
{% highlight ruby %}
xmlns:task="http://www.springframework.org/schema/task"
xsi:schemaLocation=
http://www.springframework.org/schema/task
http://www.springframework.org/schema/task/spring-task-3.0.xsd"
{% endhighlight %}

<br/>

#### 2. 스케쥴러등록
아래와 같이 스케쥴러를 등록해 준다. id는 임의로 정한다.
{% highlight ruby %}
<task:scheduler id="gsScheduler" pool-size="20" />
<task:executor id="gsTaskExecutor" pool-size="10"/>
<task:annotation-driven executor="gsTaskExecutor" scheduler="gsScheduler"/>
{% endhighlight %}

<br/>

### ▶ 스케쥴러 처리로직 작성
스케쥴러 적용 방법에는 두 가지가 있다.

<br/>

#### 1. Annotation 방법
아래와 같이 스케쥴러로 처리 메서드를 작성할 클래스를 작성하여 <font color="orange">@Scheduled</font>어노테이션을 붙이면 스케쥴러를 적용시킬 수 있다.<br/>
> 해당 클래스를 &lt;bean>이 아닌 &lt;context:component-scan>태그로 등록 시 @Component어노테이션을 클래스에 붙여주어야 등록된다.

{% highlight ruby %}
public class TaskBatch {
    @Scheduled(fixedDelay=1000)
    public void TestScheduler(){
        System.out.println("스케쥴링 호출");
    }
}
{% endhighlight %}

<br/>

#### 1-2 @Scheduled 속성
- <font color="orange">cron</font>
: 호출할 특정 시간을 지정( 초 분 시 일 월 요일 년(옵션) )<br/>
ex) @Scheduled(cron=0 45 11 * * *) => 매일 11시 45분 마다
<br/>


- 초 : 0-59 , - * / 
- 분 : 0-59 , - * / 
- 시 : 0-23 , - * / 
- 일 : 1-31 , - * ? / L W 
- 월 : 1-12 or JAN-DEC , - * /
- 요일 : 1-7 or SUN-SAT , - * ? / L #  
- 년(옵션) : 1970-2099 , - * / 

<br/>

- \* : 모든 값
- ? : 특정 값 없음
- \- : 범위 지정에 사용
- , : 여러 값 지정 구분에 사용
- / : 초기값과 증가치 설정에 사용
- L : 지정할 수 있는 범위의 마지막 값
- W : 월~금요일 또는 가장 가까운 월/금요일
- \# : 몇 번째 무슨 요일 2#1 => 첫 번째 월요일


- fixedDelay
: Task종료 시간으로부터 정의된 시간만큼 지난 후 (ms)
- fixedRate
: Task시작 시간으로부터 정의된 시간만큼 지난 후 (ms)

<br/>

#### 2. xml설정 방법
아래와 같이 스케쥴러를 등록할 때 ref로 클래스를 연결하고 메서드와 스케쥴러 옵션을 지정한다
{% highlight ruby %}
<task:scheduler id="scheduler" pool-size="2">
    <task:scheduled-tasks scheduler="scheduler">
        <task:scheduled ref="TaskTestService" method="doJob" cron="0/4 * * * * ?">
        </task:scheduled>
    </task:scheduled-tasks> 
</task:scheduler>
{% endhighlight %}




<br/>