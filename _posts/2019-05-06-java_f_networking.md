---
layout: post
title: "15. 네트워킹"
tags: [ java, tcp, udp, networking ]
date: 2019-05-06
categories: [ java ]
---

<p align="center">
    자바에서 통신은 기본적으로 TCP와 UDP로 나뉘어진다. 네트워킹 처리하는 법에 대해 알아보자.
</p><br/>

# ◆ 네트워킹  
인터넷상에 연결된 컴퓨터끼리 데이터를 주고받는 작업(통신)<br/>
- Client: 서비스를 받는 쪽 
- Server서비스를 제공하는 쪽<br/>
네트워크 통신 방식은 크게 두 가지가 있다. 

<br/>

#### ▶ TCP(Transmission Control Protocol) vs UDP(User Datagram Protocol)
차이점은 TCP는 연결 기반, UDP는 비 연결 기반의 통신이다.
- TCP
: 상대방과 <font color="orange">연결을 유지</font>하며 데이터를 주고받음. ex) 전화<br/>
( 안정적인 데이터 흐름을 보장 ) - 속도는 느림
- UDP
: 상대방과 <font color="orange">연결을 유지하지 않음</font>. 일방적으로 전송을 함. ex) 문자<br/>
( 데이터 도착에 대한 보장을 하지 않음 ) - 속도는 빠름

<br/><br/>

# ◆ UDP 통신 
UDP로 통신하기 위해서는 연결하기 위한<font color="orange">DatagramSocket</font>객체와 데이터를 전송하기 위한<font color="orange">DatagramPacket</font>객체가 필수적으로 필요하다.

#### ▶소켓 객체 생성 

{% highlight ruby %}
DatagramSocket soc = new DatagramSocket(45654); // 서버
DatagramSocket soc = new DatagramSocket();  //클라이언트
{% endhighlight %}

- DatagramSocket객체 생성
: 소켓객체의 생성은 서버와 클라이언트 모두 같은 방식으로 생성하나, <font color="orange">서버쪽에서는 포트번호가 필수</font>적으로 필요하다. 

- 클라이언트 소켓 객체 생성 시
: 통신 기지국역할을 하여 발신권이생김, 포트번호를 지정하여 생성할 수도 있지만, 미지정시 1~65535사이의 포트번호가 자동으로 지정된다.

- 서버 소켓 객체 생성 시 
: 서버쪽의 소켓객체 생성 시에는 포트번호를 꼭 지정해 주어야 클라이언트에서 포트 정보를 가지고 보낼 수 있다. ( 주의: 소켓은 while문 밖에서 선언해 줘야 한다. )

<br/><br/>

# ◆  UDP통신 패킷(=데이터) 객체 생성   

## ▶ [UDP] 클라이언트 패킷 객체 생성
클라이언트의 패킷객체 생성 시에는 4가지의 인자가 필요하다.
{% highlight ruby %}
DatagramPacket p = new DatagramPacket(송신할 byte[]배열, 송신할 길이(int), ip주소, 상대방포트번호);
{% endhighlight %}

1. 송신할 byte[] 배열
: 첫번째 인자로 byte타입의 배열이 필요하다. String타입의 데이터를 보낼경우 <font color="ornage">getBytes()</font>메서드를 통해 쉽게 byte배열로 변환이 가능하다. <br/>
ex) String req = "보낼데이터";  req.getBytes()
> int나 double등의 데이터를 보낼 때도 String형으로 변환한 다음 getBytes()메서드를 이용하여 보내면 간단하게 보낼 수 있다.

2. 송신할 길이(int)
: 송신할 길이를 int형으로 기입한다. 모두 보낼 시에는 byte[]배열의 lentgh만큼 쓰고, 아닐 경우 보낼 만큼 쓴다.
  
3. ip주소(InetAddress객체)
: ip주소는 단순한 String으로 보낼 수 없고 <font color="orange">InetAddress객체</font>를 인자로 보내야 한다.<br/>
InetAddress addr = InetAddress.getByName("192.168.10.61"); 로 생성

4. 상대방의 포트번호 int형
: 송신할 때 상대방의 ip주소와 포트번호를 알아야 하기 때문에 포트번호를 int형으로 적어준다.<br/>
(서버의 포트번호를 지정해 주어야 하는 이유)

<br/>

#### ▶ ip와 포트번호 동시 설정
ip주소와 상대방의 포트번호를 따로 입력하는 것이 번거롭기 때문에 <font color="orange">SocketAddress</font>객체를 이용하여 한 번에 입력도 가능하다.
<br/>
즉, Datagrampacket객체를 생성할 때 인자를 3개로 보낼 수 있다.
{% highlight ruby %}
SocketAddress address = 
new InetSocketAddress("192.168.10.61"(스트링) 또는 InetAddress객체, 포트번호(int));
{% endhighlight %}
객체는 SocketAddress지만, 생성은 new InetSocketAddress()를 이용하기 때문에 주의

<br/>

## ▶ [UDP]서버 패킷 객체 생성 시
서버의 패킷은 데이터를 수신할 용도로 사용하기 때문에 IP주소와 포트번호를 지정해 줄  필요가 없고,<br/>
데이터를 담을 byte[]배열을 적어주면 해당 배열로 데이터가 담겨온다.
{% highlight ruby %}
byte[] re_data = new byte[100]; // 길이는 넉넉하게 잡아두는 것이 좋음
DatagramPacket p = new DatagramPacket(re_data, 받아올 길이);
{% endhighlight %}

> 서버쪽에서는 클라이언트의 수신을 받을 시 클라이언트의 ip주소와 포트번호를 알 수 있기 때문에 응답할 때도 이를 이용하여 같은 방식으로 보낼 수 있다.

<br/>
# ◆ [UDP] DatagramSocket객체 메서드
- socket.send(DatagramPacket객체);  
: 만들어진 패킷의 정보를 소켓을 통해 보냄.
<br/>
( 이때 클라이언트의 ip주소와 포트 번호가 패킷에 같이 묶여서 전달됨, 
따라서 서버는 수신한패킷객체.getSocketAddress()로 클라이언트의 주소 정보를 알 수 있다. )
  
- socket.receive(DatagramPacket객체); 
: 송신된 데이터를 매개변수의 패킷 객체생성 시 지정한 byte[]배열로 받아옴.<br/>
=> receie()메서드는 클라이언트에서 패킷이 날아올 때 까지 대기상태에 빠져있는다.
<br/>
> 받아온 데이터는 byte[]배열이므로 new String(byte[]배열)를 통해 볼 수 있다<br/>
단, 이때 받아온 데이터의 길이는 패킷객체에서 설정한 받는 길이이기 때문에 <font color="orange">new String(byte[] b , 0 , 패킷객체.getLength())</font> 만큼만 변환해야한다.

- 소켓객체.getLocalPort()
: 소켓객체에 생성된 포트번호를 반환
- 소켓객체.setSoTimeout(5000);  
: 5000ms 동안 응답이 없으면 종료 <br/>
Client측에서는 필요한 코드 (Server쪽에선 하지 않는다 )
- 소켓객체.close()
: 서버 측에서 while반복문을 통해 무한으로 서버를 켜두기 때문에
반복문 밖에서 미리 null로 선언하고 finally 문에서 닫도록 한다!

<br/>

# ◆ [UDP] DatagramPacket객체 메서드
  
- pacekt.getData(); 
: 받아온 패킷의 데이터를 byte[]배열로 반환<br/>
생성 시 설정한 byte[]배열로 데이터가 담겨져 오지만 해당 메서드를 이용하여 반환받을 수도 있다.

- 패킷객체.getLength(); 
: 받아온 패킷의 실제길이를 반환 <br/>
서버에서는 패킷에 설정한 만큼 받아오기 때문에 이 길이를 알아야 실제 데이터의 길이를 알 수 있다.

- 패킷객체.getAddress() 
: 수신한 패킷의 송신 쪽 ip주소를 InetAddress객체로 반환
- 패킷객체.getPort()
: 수신한 패킷의 송신 쪽 포트번호를 반환
- 패킷객체.getSocketAddress()
: 수신한 패킷의 송신 쪽 아이피와 포트번호 정보가 있는 SocketAddress객체 반환

<br/>

## ▶ UDP통신예제
예제에서는 main메서드 안에서 서버와 클라이언트 모두 실행하였지만, 실제로는 프로그램을 나누어 서버와 클라이언트가 분리되어 작동하는 방식으로 사용된다.

{% highlight ruby %}
try {
    DatagramSocket server = new DatagramSocket(7001);
	DatagramSocket client = new DatagramSocket();
			
	// 클라이언트 패킷
	// 클라이언트 전송용 패킷
	DatagramPacket c_dp = new DatagramPacket
        ("client send".getBytes(), 11, new InetSocketAddress("localhost", 7001));
    // 클라이언트 수신용 패킷
	byte[] c_data = new byte[100];
	DatagramPacket c_re_dp = new DatagramPacket(c_data, 100);
			
    // 서버 패킷
	// 서버 수신용 패킷
	byte[] s_data = new byte[100];
	DatagramPacket s_dp = new DatagramPacket(s_data, 100);
			
	client.send(c_dp);
	server.receive(s_dp);
			
	System.out.println("수신된 데이터 : " + new String(s_dp.getData(), 0, s_dp.getLength()));
	System.out.println("=> 수신된 패킷 정보");
	System.out.println("포트 : " + s_dp.getPort());
	System.out.println("주소 : " + s_dp.getAddress());
			
	// 서버응답
	// 서버 전송용 패킷 생성
	String s_re = new String(s_dp.getData(),0,s_dp.getLength()) + "=> server response";
    DatagramPacket s_send_p = 
        new DatagramPacket(s_re.getBytes(), s_re.length(), s_dp.getSocketAddress()); 
    // getSocketAddress를 이용하여 클라이언트의 ip주소와 포트를 한번에 받아옴
    
    server.send(s_send_p);
			
    // 클라이언트 응답 수신
	client.receive(c_re_dp);
	System.out.println(new String(c_re_dp.getData(), 0, c_re_dp.getLength()));
			
	server.close();
	client.close();
			
} catch (Exception e) {
    e.printStackTrace();
}
{% endhighlight %}

<br/>

# ◆ TCP통신 
연결을 유지한 상태로 데이터를 주고받음(연결 기반), 때문에 UDP는 보통 서브로 사용됨
- 애초에 연결이 안 되면 데이터를 주고받을 수가 없음.
- Socket이란 클래스가 사용됨.
- UDP는 패킷으로 통신을 하지만, TCP는 <font color="orange">(in/out)putStream객체로 통신</font>을 한다.

<br/>

#### ▶ 서버 소켓
서버소켓의 생성은 <font color="orange">ServerSocket</font>객체로 서버의 소켓을 생성하여 통신할 포트를 열어준다.
{% highlight ruby %}
ServerSocket server = new ServerSocket(45678);
{% endhighlight %}
UDP와 마찬가지로 port가 필요함(개방할 port) - 클라이언트와 통신할 포트 설정
- Connect Exception : 연결 거절당했을 때
- UnknownHostException : 서버 측의 IP가 잘못 설정되었을 때

<br/>

#### ▶ 클라이언트 소켓
클라이언트의 소켓생성은 <font color="orange">Socket</font>객체를 이용하며, 인자로는 연결할 서버의IP주소(String)와 포트번호이다.
{% highlight ruby %}
Socket soc = new Socket("192.168.10.80", 45678);
{% endhighlight %}
생성 자체가 연결시도 Socket(String host, int port)서버 측의 Address 설정

<br/>

#### ▶ In/Out putStream 객체
{% highlight ruby %}
OutputStream os = soc.getOutputStream();
InputStream is = soc.getInputStream();
{% endhighlight %}
소켓객체 생성 시 연결되면서 생성되는 IO객체를 단순히 뽑아서 쓰는 형태.(new를 이용해서 생성할 필요가 없다.)<br/>

> 클라이언트에서 output을 열면 서버에서는 input을 열어 줘야하고, 반대상황에서는 반대로 열어 줘야한다. ( 따라서 동시에 input이나 output을 열게 되면 오류! )
  
#### 입출력보조 활용
File의 입출력 보조 클래스처럼 네트워킹에서도 좀 더 쉽게 입출력 할 수 있는 보조 클래스를 제공한다.<br/>
In/OutputStream을 인자로 하는 Data(In/Out)putStream 또는 Object(In/Out)putStream이 있다.
{% highlight ruby %}
OutputStream os = soc.getOutputStream();
ObjectOutputStream oos = new ObjectOutputStream(os); 
oos.writeObject("오브젝트");  
// 서버에선 is.readObject()로 받아준다.
{% endhighlight %}

<br/>

#### ▶ Socket server_soc = server.accept();
서버 측에서 쓰이는 메서드로, 대기상태에서 접속을 기다리다가, 연결 발생 시 <font color="orange">연결 시도한 대상과 데이터를 주고받을 소켓을 생성</font>시킴( 즉 실제 연결되는 지점 )<br/>
=> accept()를 호출하지 않은 상태에선 연결을 할 수 없다.

#### ▶ TCP통신 예제
마찬가지로 Server와 Client의 프로그램을 따로 만드는것이 일반적이다.
{% highlight ruby %}
try {
    ServerSocket server = new ServerSocket(7001);
    Socket client = new Socket("localhost",7001); // 서버와 연결시도
			
	Socket server_socket = server.accept(); // 연결
	System.out.println("연결성공");
			
	OutputStream os = client.getOutputStream();
	os.write("client send".getBytes());
			
	InputStream is = server_socket.getInputStream();
	byte[] data = new byte[100];
	int data_len = is.read(data);
	System.out.println("클라이언트 전송정보 : " + new String(data, 0, data_len));

} catch (Exception e) {
	e.printStackTrace();
}
{% endhighlight %}

#### ▶ 동시처리
TCP는 기본적으로 1:1 통신이기 때문에 연결된 상태로 상대방과의 통신을 처리하는 방식이라 차례대로 처리가 되기 때문에 동시 처리가 불가능하다.
<br/>
따라서 TCP방식으로 <font color="orange">다중클라이언트를 동시 처리 하려면 멀티 쓰레드로 구현해야 한다!</font>
<br/>
=> 하나의 클라이언트와 연결되고, 언제 통신이 끊기는지 모르기 때문에 연결된 클라이언트와의 작업을 또 하나의 try~catch반복문으로 익셉션 발생 시 소켓을 닫아주는 방법으로 통신을 끊을 수 있다. 
<br/>( 이중 반복, 이중 try~catch )<br/>
 주의 ) 소켓, 인풋아웃풋 스트림은 반복문 안에서 생성하지 않는다.

> 프로젝트가 다른 곳에서 같은 클래스로 인식되게 하고 싶으면 버전ID를 설정해두면 됨. 물론 같은 위치로 설계가 된 상태여야 함.<br/>
=> private static final long serialVersionUID = 1L;<br/>
( 단 서버 측의 본래 코드와 가져온 코드가 완전히 같아야 한다.(주석 빼고 모두) 즉 서버측에서도  private static final long serialVersionUID = 1L








<br/>