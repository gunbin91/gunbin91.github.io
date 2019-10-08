---
layout: post
title: "14. Spring Web Socket"
tags: [ spring, websocket ]
date: 2019-10-02
categories: [ spring ]
---

<p align="center">
    
</p><br/>


## ◆ SPRING WEB SOCKET
스프링은 별도의 웹 소켓 서버를 설치하지 않아도 웹 소켓 기능을 사용할 수 있게 지원한다.<br/>
웹 소켓 API를 사용하게 되면 <font color="orange">서버에서 클라이언트로 먼저 응답을 보내는 것이 가능</font>해진다.<br/>

> 웹 소켓은 채팅기능 구현에 주로 쓰일 수 있는데, 웹 소켓 없이 만들경우 setInterval스크립트 함수를 이용하여 구현할 수 있지만 요청이 많아지기 때문에 과부하가 생길 수 있다.

- setInterval 예 )
{% highlight ruby %}
function receiveMsg() {
	$.get("showMsg", function(data) {
		var obj = JSON.parse(data);
		var content = "";
		for (var i = 0; i < obj.length; i++) {
            content += "<font color='blue'>" + obj[i].id + "</font> : "
            + obj[i].msg + "<br/>";
		}
		$("#chatDIV").html(content);
	});
}

setInterval(receiveMsg, 1000); // 초당 한번씩 호출
{% endhighlight %}
위와 같이 계속해서 상태를 요청하여 받아오게 되면 과부하가 발생할 수 있다.<br/>
하지만 웹 소켓을 이용하게 되면 다른 클라이언트의 요청 발생시에만 모든 클라이언트의 상태를 갱신할 수 있기 때문에 과부하가 발생할 확률이 적다.

<br/>

### ▶ 라이브러리 연동
Spring은 WAS를 가지고도 웹 소켓 서버의 기능을 구현할 수 있게 해두었음.

-메이븐추가( Spring WebSocket )
: {% highlight ruby %}
<!-- https://mvnrepository.com/artifact/org.springframework/spring-websocket -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-websocket</artifactId>
    <version>4.3.14.RELEASE</version>
</dependency>
{% endhighlight %}

<br/>

### ▶ 웹 소켓 처리 컨트롤러 작성방법
웹 소켓을 처리할 컨트롤러는 두 가지 방식으로 처리할 수 있다

#### 1. WebSocketHandle를 implements걸어서 목적에 맞게 개조해서 사용.
#### 2. 목적에 맞는 WebSocketHandler를 extends걸어서 사용
- 문자처리 : TextWebSocketHandler
- 파일처리 : BinaryWebSocketHandler

<br/>

## ◆ TextWebSocketHandler를 이용한 WebSocket통신
TextWebSocketHandler를 extends하여 생성한 컨트롤러는 afterConnectionEstablished, handleTextMessage, afterConnectiopnClosed 메서드를 Override해야 한다.

<br/>

### ▶ 컨트롤러 작성 예제
{% highlight ruby %}
@Controller("wsc")
public class WSController extends TextWebSocketHandler {
    // 각각 클라이언트의 WebSocketSession객체를 저장할 Set객체
	Set<WebSocketSession> wsSession;

	@PostConstruct // init-method
	public void init() {
		wsSession = new LinkedHashSet<>();
	}

    // (클라이언트와)연결 되었을 때 호출
	@Override
	public void afterConnectionEstablished(WebSocketSession session) throws Exception {
    // 클라이언트들에게 메시지 전달 후 Set에 클라이언트하나 추가
		for (WebSocketSession ws : wsSession) {
            // 해당 ws객체에 해당하는 소켓으로 메시지 전달
			ws.sendMessage(new TextMessage("oepn"));
		}
		wsSession.add(session);
	}

    // (클라이언트와)메시지를 보낼 때 호출
	@Override
	protected void handleTextMessage(WebSocketSession session, TextMessage message) throws Exception {
		for (WebSocketSession ws : wsSession) {
			ws.sendMessage(new TextMessage("send"));
		}
	}

    // (클라이언트와)연결 해제 시
	@Override
	public void afterConnectionClosed(WebSocketSession session, CloseStatus status) throws Exception {
        // Set에서 클라이언트 해제 후 나머지클라이언트에게 메시지 전달.
		wsSession.remove(session);
		for (WebSocketSession ws : wsSession) {
			ws.sendMessage(new TextMessage("close"));
		}
	}
}
{% endhighlight %}
- 해당 메서드에서의 session은 HTTPSESSION객체와는 전혀 다른 객체이다.
- 자동 등록되는 객체들은 init-method를 설정할 타이밍이 없기 때문에 init()메서드를 만들어서 @PostConstruct 어노테이션을 붙여주면 init메서드로 설정된다.
- session.sendMessage(new TextMessage(""));메서드로 메시지를 전달할 수 있다.
- session.getRemoteAddress().getAddress().getHostAddress() : 클라이언트 ip반환

<br/>

### ▶ 웹 소켓 핸들러 등록
웹 소켓 컨트롤러의 경우 경로를 @RequestMapping을 통해서 지정하는 것이 아니라 스프링 설정파일에서 빈 객체를 등록 할 때 경로를 설정할 수 있다. 단 접근은 Websocket을 통해서만 할 수 있다.

#### 1. 스프링설정파일 -> Namespaces -> websocket 체크
#### 2. <websocket:handlers>태그를 이용하여 핸들러 등록
{% highlight ruby %} 
<websocket:handlers>
    <websocket:mapping handler="WSController" path="/handle" />
</websocket:handlers>
{% endhighlight %}
- handler옵션으로 컨트롤러의 id를 적어주고(ref), path에 접근(매핑) 경로를 적어준다.

> &ltcontext:component-scan>으로 등록된 컨트롤러들은 자동으로 클래스이름(또는 앞에만 소문자)를 id로 갖는다.<br/>
또는 @Controller("id")형식의 어노테이션을 이용 하는것도 가능하다.

<br/>

### ▶스크립트를 이용하여 웹 소켓 연결
웹 소켓 컨트롤러와 클라이언트를 연결하기 위해서는 스크립트를 통하여 연결을 시켜야 한다.

- 소켓 연결
: <font color="orange">new WebSocket("ws:// ip(:port)/수정경로/컨트롤러경로");</font>
{% highlight ruby %}
<script>
    var ws = new WebSocket("ws://${pageContext.request.serverName}/handle");
</script>
{% endhighlight %}
=> ${pageContext.request.serverName}은 서버의 ip를 반환해준다.

- 연결이 됐을 때( onopen )
: {% highlight ruby %}
ws.onopen = function() {
    console.log("onopen");
    console.log(this);
}
{% endhighlight %}

- 메시지가 들어올 때( onmessage )
: {% highlight ruby %}
ws.onmessage = function(obj) {
    window.alert(obj.data);
}
{% endhighlight %}
obj.data로 서버에서 보낸 메시지를 확인할 수 있다.<br/>
( GSON으로 메시지를 보냈을 때 JSON.parse(obj.data)를 이용하여 사용할 수도 있다.  )

- 연결이 끊길 때 ( 서버가 꺼질 때 )
: {% highlight ruby %}
ws.onclose = function() {
    window.alert("연결이 해제되었습니다.");
}
{% endhighlight %}

- 메시지 보내기
{% highlight ruby %}
ws.send(“msg”);
{% endhighlight %}
위 처럼 스크립트를 통해 메시지를 보낼 수도 있지만, 소켓 컨트롤러의 각 클라이언트의 WebSocketSession객체를 따로 저장하여 서비스객체를 통해 메시지를 보낼 수도 있다.

<br/>

> ※ 주의  <br/>
한 페이지에서 스크립트를 이용해 소켓을 생성할 시 <font color="orange">다른 페이지로 넘어갈 때 해당 소켓과의 연결이 해제</font> 된다. 따라서 <font color="orange">여러 페이지에서 소켓통신을 사용해야 할 경우 각 페이지마다 소켓을 생성하거나, 소켓을 생성하는 페이지를 include</font>시켜야 한다.<br/>
=> 즉 여러 페이지에서 소켓을 생성할 시 연결/해제를 반복하며 통신이 이루어진다. 따라서 연결된 WebSocketSession객체를 컨트롤러에 저장할 때도 연결될 때마다 새로 저장시키게 된다.

<br/>

### ▶ 웹 소켓 컨트롤러에서 HttpSession가져오기
웹 소켓을 처리하는 컨트롤러에서는 메서드의인자로 HttpSession객체를 가져 올 수 없다.<br/>
따라서 HttpSession객체를 제어할 수 없기 때문에 <font color="orange">웹 소켓 컨트롤러에서 HttpSession객체의 데이터가 필요한 경우 설정이 필요</font>하다.<br/>
( 단, 실제로 HttpSession객체를 가져오는 것이 아닌 <font color="orange">세션이 가지고 있는 데이터만을 불러오는 것</font>이기 때문에 세션객체를 제어할 수는 없다. )

#### 1. 스프링 설정파일 수정
등록한 웹 소켓 컨트롤러에 handshke-interceptiors를 이용하여 HttpSessionHandshakeInterceptor를 등록한다. <br/>( HttpSession 객체를 가로채기 )
{% highlight ruby %}
<websocket:handlers>
    <websocket:mapping handler="ac" path="/alert" />
    <websocket:handshake-interceptors>
        <beanclass="org.springframework.web.socket.server.support.HttpSessionHandshakeInterceptor"></bean>
    </websocket:handshake-interceptors>
</websocket:handlers>
{% endhighlight %}

<br/>

#### 2. HttpSession객체 가져오기
위 1번처럼 등록을 하게 되면 session.getAttributes();를 이용하여 Map<String,Object>형태로 HttpSession객체를 가져올 수 있다.
<br/><br/>
로그인된 사용자의 socket을 저장하는 예)
{% highlight ruby %}
public class SocketController extends TextWebSocketHandler {

	@Autowired
	SocketService socketService;

	// (클라이언트와)연결 되었을 때
	@Override
	public void afterConnectionEstablished(WebSocketSession session) throws Exception {
		// 로그인 아이디 - WebSocket 등록
		Map map = session.getAttributes();
		if (map.get("logon") != null) {
			socketService.addSocket((String) map.get("logon"), session);
		}
	}
    
}
{% endhighlight %}
서비스객체로 WebSocketSession객체를 넘겨주어 따로 저장한다.




<br/>