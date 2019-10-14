---
layout: post
title: "10. MVC패턴 구현 지원 Controller2<br/> [ @RequestMapping, 매개 인자 셋팅 ]"
tags: [ spring, controller ]
date: 2019-09-19
categories: [ spring ]
---

<p align="center">
    Spring Controller또한 서블릿에서 사용하던 모든 기능을 사용할 수 있다.<br/>
</p><br/>

## ◆ @RequestMapping() 

<br/>

### ▶ 같은 경로의 @RequestMapping()을 가진 메서드를 작성할 수 없다.
하나의 컨트롤러에 여러 개의 @RequestMapping()을 붙인 메서드를 만들 수는 있지만,<br/>
같은 경로로 여러 개의 메서드를 만들 수는 없다. 또는 같은 경로의 다른 컨트롤러 또한 불가능하다.<br/>
( 단, method방식이 다른 접근일 경우에는 가능하다. )

<br/>

### ▶ 하나의 메서드 또는 하나의 컨트롤러에 여러 개의 경로를 잡을 수도 있다.
경로를 중괄호{}로 묶어 여러 경로를 하나의 메서드로 매핑시킬 수 있다. <br/> <font color="orange">@RequestMapping( { "/bye", "/out" } )</font> 형식으로 콤마(,)를 구분자로 하나의 메서드 또는 클래스에 여러 경로를 잡을 수도 있다.

<br/>

### ▶ @RequestMapping에는 몇 개의 설정 옵션이 있다.
여러 개의 옵션을 설정할 때는 콤마(,)를 구분자로 설정해준다.<br/>
- path 
: 인자로 경로만 적어줄 때에는 디폴트로 설정되어 있기 때문에 적어줄 필요가 없지만 <font color="orange">여러개의 인자를 작성할 경우 path옵션을 통해 경로를 적어준다.</font>
- method 
: <font color="orange">RequestMethod.GET / RequestMethod.POST</font> 로 접근 메서드형식을 지정할 수 있고, 해당 메서드가 다른 접근일 때는 같은 경로로 설정이 가능하다.
ex ) 
{% highlight ruby %}
@RequestMapping(path = "/alpha/03", method = RequestMethod.POST)
{% endhighlight %}

<br/>

### ▶ @RequestMapping의 경로를 메서드의 인자로 받을 수 있다.
Spring에서는 접근경로를 동적으로 사용할 수 있고, 이를 변수로 활용할 수도 있다.<br/> <font color="orange">@RequestMapping("/{경로변수}")</font>로 경로를 중괄호로 묶어주게 되면, <font color="orange">해당 자리는 어떤 경로로 접근을 하던 처리가 가능해지고, 설정한 부분의 경로를 인자로</font> 받을 수 있게된다.

- 접근경로를 인자로 받아오는 방법 
: 컨트롤러 메서드의 인자로 <font color="orange">@PathVariable라는 어노테이션을 이용하여 설정한 접근 경로값을 매개인자로 받아올 수 있다.</font><br/> 단, @RequestMapping( "/{ 변수 }" ) 에서 설정한 변수와 메서드의 변수명을 일치시켜야 한다. 
{% highlight ruby %} 
@Controller
@RequestMapping("/beta")
public class BetaController {
    @RequestMapping("/{subject}")
    public void betaSubjectHandle(@PathVariable String subject) { 
        System.out.println("BetaController" + subject);
    }
}
{% endhighlight %}
/beta/test로 접근하게 되면 subject값으로 test가 들어오게 된다.

- 이중경로처리는 불가능 ex) /beta/alpha (O), /beta/alpha/brabo (X)

- 여러 경로로 설정도 가능
: {% highlight ruby %}
@RequestMapping("/{type}/search/{no}")
public void betaTypeHandle(@PathVariable String type, @PathVariable("no") String n) {
    System.out.println("BetaController" + type + " / " + n);
}
{% endhighlight %}
search를 제외한 {type}과 {no}자리에는 어떤 경로로도 접근이 가능하다.

- 위처럼 인자로 @PathVariable등의 어노테이션 변수를 설정할 때 <font color="orange">@Pathvariable("변수") 로 미리 일치하는 값을 지정해두면, 인자 값을 { }안의 변수와 일치시킬 필요는 없다.</font>

<br/>

### ▶ @RequestMapping()를 메서드가 아닌 컨트롤러 클래스 위에 적어주어도 된다.
@RequestMapping을 컨트롤러 클래스 위에 적어도 컨트롤러 메서드에서 또 다시 정의해 줄 수 있다.<br/>
단, 이렇게 <font color="orange">이중으로 정의할 경우 클래스에서 정의한 경로의 하위경로로 설정</font>된다.
{% highlight ruby %}
@RequestMapping("/beta")
public class BetaController {
    // ~/beta 가 GET방식일 때
    @RequestMapping(method = RequestMethod.GET)
    public void betaGetHanle() {
        System.out.println("BetaController.betaGetHandle() called");
    }
    // ~/beta 가 POST방식일 때
    @RequestMapping(method = RequestMethod.POST)
    public void betaPostHanle() {
        System.out.println("BetaController.betaPostHandle() called");
    }
    // ~/beta/new 일 때
    @RequestMapping(path = "/new")
    public void betaNewHandle() {
        System.out.println("BetaController.betaNewHandle() called");
    }
}
{% endhighlight %}
=> betaNewHandle()의 접근경로는 /beta/new

<br/>

### ▶ 메서드명을 경로로 사용( 경로 없는 @RequestMapping구조 )
컨트롤러 <font color="orange">클래스의 @RequestMapping의 경로가 /*</font>로 끝나는 경우 컨트롤러 메서드위에 @RequestMapping어노테이션만 붙이게 되면, <font color="orange">메서드명 자체가 *에 해당하는 접근 경로</font>가 된다.

{% highlight ruby %}
@RequestMapping("/user/*")
public class UserController  {
     // /user/add 접근 시 호출
     @RequestMapping
     public String add(...) {}
     
     // /user/edit 접근 시 호출
     @RequestMapping
     public String edit(...) {}
}
{% endhighlight %}

<br/>

## ◆ 컨트롤러 메서드의 매개인자
어노테이션 기반의 컨트롤러 메서드는 정해진 형식이 없기 때문에 여러 가지 형태로 매개변수를 받을 수 있다.

<br/>

#### ▶ 넘겨줄 데이터를 설정하는 Map
컨트롤러 메서드 매개 인자로 Map을 설정하게 되면 <font color="orange">Map객체.put("키","벨류")하여 데이터를 포워딩페이지로 넘겨줄 수 있다.</font> request.setAttribute와 같은 기능
{% highlight ruby %}
map.put("data","100"); // send
request.getAttribute("data"); // receive
{% endhighlight %}

<br/>

#### ▶ 넘겨줄 데이터를 설정하는 Model ( org.springframework.ui.Model )
Model객체는 <font color="orange">Map객체를 인자로 받을 때와 같은 기능</font>을 하지만 메서드는 다르다. <br/><font color="orange">Model객체.addAttribute("키","벨류")</font>를 설정하게 되면 request.getAttribute("키")로 받을 수 있다.<br/>
( Model객체의 패키지가 springframework의 Model객체가 맞는지 주의 )
{% highlight ruby %}
Model.addAttribute("data","100"); //send
request.getAttribute("data"); // receive
{% endhighlight %}

<br/>

#### ▶ 넘겨줄 데이터를 설정하는 ModelMap
ModelMap객체는 <font color="orange">Map객체와 Model객체가 합쳐진 형태</font>로 편의를 위해 만들어진 객체이다.<br/>
ModelMap객체.put("키","벨류"), ModelMap객체.addAttribute("키","벨류") <font color="orange">두 개의 메서드 모두 사용이 가능</font>하다.
{% highlight ruby %}
// send
ModelMap.put("data","100");
ModelMap.addAttribute("msg","HI");
// receive
request.getAttribute("data");
requeest.getAttribute("msg");
{% endhighlight %}

> 데이터를 넘겨줄 수 있는 객체를 이렇게 <font color="orange">Map, Model, ModelMap</font>객체가 있다.<br/>본인이 사용하기 편한 객체를 골라서 쓰면 된다.

<br/>

#### ▶ Request와 Response객체 받아오기
서블릿과 마찬가지로 컨트롤러 메서드에서도 인자로 <font color="orange">ServletRequest 또는 HttpServletRequest</font>를 받게 되면 Request객체 또는 Response객체를 받을 수 있게 된다.
<br/>( javax.servlet.http.HttpServletRequest )

<br/>

#### ▶ Session객체 받아오기
Session객체는 request.getSession()으로 뽑아서 써도 되지만, <font color="orange">HtpSession객체를 받게 되면 알아서 session객체를 뽑아</font>서 주게 된다.<br/>

> servletContext(application)객체는 매개인자로 넘겨주는 것을 지원하지 않기 때문에 request.getServletContext()로 뽑아서 써야한다.

<br/>

#### ▶ 파라미터값 불러오기 @RequestParam
request.getParameter()를 사용하지 않고 어노테이션 "<font color="orange">@RequestParam 타입 변수명</font>"을 이용하여 파라미터를 받을 수 있도록 지원한다. ( Post방식도 가능 )

- 기본 사용 방식 : @RequestParam String id
- 파싱 가능 : @RequeestParam <font color="orange">int</font> id ( 단, 잘못된 파싱일 시 오류 )
- 설정한 파라미터를 넘겨주지 않을 경우 에러가 발생( null 또는 default값으로 처리 필요 )
- 파라미터값을 디폴트 null로 설정 가능 : @RequestParam<font color="orange">(required=false)</font> String id
- 또는 파라미터의 디폴트 값 설정 가능 : @RequestParam<font color="orange">(defaultValue="1")</font> String id
- request.getParameterValues()도 가능 : @RequestParm("id") <font color="orange">String[]</font> id
{% highlight ruby %}
@RequestMapping("/01")
public void eta01Handler(
    @RequestParam(required = false) String id, 
    @RequestParam String pass,
    @RequestParam(defaultValue = "1") int mode, 
    @RequestParam("concern") int[] concern ){ 
    ... 
}
{% endhighlight %}
※ 변수 값과 일치하는 값을 써야하는 매개변수명은 어노테이션 뒤에 미리 설정해두면 같은 변수 명을 사용하지 않아도 된다.
{% highlight ruby %}
@RequestParam("id") String s
{% endhighlight %}

<br/>

#### ▶ Map으로 파라미터 담아오기 @RequestParam Map
&nbsp;<font color="orange">@RequestParam의 타입을 Map으로 지정하면 모든 파라미터를 하나의 Map객체</font>로 받을 수 있다.<br/> 
단 제네릭 형태는 <String,String>으로만 된다.<br/>
( 포워딩 데이터를 설정하는 Map과 혼동하여 쓰지 않도록 주의가 필요하다. )
{% highlight ruby %}
@RequestMapping("/test2")
public String test(Map map, @RequestParam Map paramMap) {
    map.put("data","100"); // test.jsp페이지로 data데이터를 넘긴다
    paramMap.get("msg"); // 파라미터를 받는다.
    return "test.jsp";
}
{% endhighlight %}

<br/>

#### ▶ 다중value값 Map @RequestParam MultiValueMap
단일 벨류가 아닌 여러개의 값을 가지고 있는 <font color="orange">다중 벨류값</font>의 경우 단순히 타입을 배열로 받으면 되지만,<br/> 이를 <font color="orange">Map객체로 받을 경우 타입을 MultiValueMap</font>으로 바꿔 주어야 한다.<br/>
이 객체는 제네릭으로 <String,String>을 사용하지만 실제로는 <String, List<String>> 형태로 받아오게 된다.
{% highlight ruby %}
@RequestParam MultiValueMap multiMap    
{% endhighlight %}

<br/>

#### ▶쿠키값을 가져오는 @CookieValue
&nbsp;<font color="orange">@CookieValue</font>를 이용하여 변수명과 킷값을 일치시켜 해당 <font color="orange">쿠키값</font>을 가져올 수 있다.<br/>
( 쿠키 객체를 가져오는것이 아님 )
{% highlight ruby %}
@CookieValue("lastId") String id
{% endhighlight %}
- lastId에 해당하는 쿠키 값을 가져올 수 있다.
- 쿠키 또한 값이 없을 경우 터지기 때문에 @CookieValue(name="lastId",required=false) String id를 이용하여 디폴트값을 null로 설정한다.

<br/>

#### ▶ @ModelAttribute
커스탬 객체를 이용하여 파라미터를 받아오는 방법이다.<br/>
받아올 파라미터값과 일치하는 변수명의 필드를 가진 커스텀객체를 만들어 두고,<br/> <font color="orange">“@ModelAttribute 커스텀클래스 변수명”</font>을 인자로 할 경우 해당 객체에 파라미터와 일치하는 필드 값에 파라미터 값이 담겨지게 된다.
{% highlight ruby%}
String name;
int age;
boolean married;
{% endhighlight %}
위와 같은 필드를 가진 Complex객체를 만들고 모든 필드에 대한 getter, setter를 만든다.<br/> 
컨트롤러 메서드에서 <font color="orange">@ModelAttribute Complex cx</font>를 매개인자로 받게되면 자동적으로 필드명과 일치하는 값들이 셋팅되고 <font color="orange">컨트롤러에서 cx변수로 제어가 가능</font>하다.<br/>
<br/>
또한 이렇게 커스텀객체를 이용하여 파라미터를 받아오게 되면 <font color="orange">포워딩된 페이지로 해당 객체를 보내지 않아도
    request.getAttribute("complex")로 해당 객체를 불러올 수 있다.</font><br/>
( 클래스명소문자로 jsp에서 뽑아낼 수 있게 된다. )<br/>
=> 또는 @ModelAttribute("cx") 로 처리했다면 request.getAttribute("cx")로 받아야 한다.



<br/>