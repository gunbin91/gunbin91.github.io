---
layout: post
title: "18. 인터셉터(Interceptor)"
tags: [ spring, interceptor ]
date: 2019-11-05
categories: [ spring ]
---

<p align="center">
    
</p><br/>

## ◆ 인터셉터( Interceptor )
웹 요청 시 <font color="orange">Controller로 가는 요청을 가로 채 전후 처리</font>를 할 수 있도록 하는 역할

<br/>

### ▶ 인터셉터와 필터의 차이?
필터 역시 전/후처리를 하는 역할로 인터셉터와 같은 기능을 수행하지만 둘의 특징에 따라 사용하는 용도가 조금 달라질 수 있다.<br/>
( 필터는 주로 문자 인코딩 설정등에 사용됨 )

- 실행 시점이 다르다.
: Spring MVC request life cycle
Request -> <b style="color:purple">Filter</b> -> DispatcherServlet ->  Controller/<b style="color:purple">Interceptor</b>

<br/>

- 접근영역이 다르다.
: Fileter는 웹 어플리케이션에 등록(web.xml)하고, Interceptor는 Spring Context에 등록한다.

<br/>

### ▶ 인터셉터 설계

#### 1. HandlerInterceptor구현 또는 <font colorr="orange">HandlerInterceptorAdapter</font>를 상속하는 클래스 작성

<br/>

#### 2 메서드 설계
- public boolean <font color="hotpink">preHandle</font>(HttpServletRequest request, HttpServletResponse response, Object handler)
: <font color="orange">Controller가 실행되기 전</font> 실행되는 메서드 true를 리턴할 경우 Controller로 요청을 보낸다.

- &nbsp;<font color="hotpink">postHandle</font>(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView)
: <font color="orange">Controller가 실행된 후</font> View렌더링 직전 호출 매개인자의 ModelAndView객체에 Controller가 넘겨주는 값들이 저장된다.

- afterCompletion()
: View(화면)처리까지 끝난 후에 호출

<br/>

#### 3. Spring Context에 등록
인터셉터가 적용될 경로와 함께 등록 시켜주도록 한다.

{% highlight ruby %}
<!-- 인터셉터 객체 생성 -->
<bean id="ti" class="interceptors.TestInterceptor"/>

<!-- Interceptor 설정 -->
<interceptors>
    <interceptor>
        <mapping path="/board/register"/>
        <mapping path="/board/modify"/>
        <mapping path="/board/delete"/>
        <beans:ref bean="ti"/>
    </interceptor>
</interceptors>
{% endhighlight %}

<br/>

#### ▶ ex
{% highlight ruby %}
public class TestInterceptor extends HandlerInterceptorAdapter{

    @Override
    public boolean preHandle(HttpServletRequest request, 
    HttpServletResponse response, Object handler) throws Exception {
        HttpSession session = request.getSession();
        Object obj = session.getAttribute("login");
         
        if ( obj ==null ){
            response.sendRedirect("/login");
            return false; 
        }
        return true;
    }
}
{% endhighlight %}




<br/>