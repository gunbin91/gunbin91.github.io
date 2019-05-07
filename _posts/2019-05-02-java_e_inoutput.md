---
layout: post
title: "14. 입출력(Input/Output)"
tags: [ java, file input, file output ]
date: 2019-05-02
categories: [ java ]
---

<p align="center">
    외부로 부터 데이터를 받아들이는 작업을 입력(Input)이라 하고, 외부로 데이터를 빼내는 것을 출력(Output)이라고 한다.
</p><br/>

# ◆ 파일 입출력
- 입력? 
: 데이터를 받아들이는 작업 (Input) // 파일 -> 프로그램<br/>
- 출력?
: 데이터를 내보내는 작업 (Output) // 프로그램 -> 파일<br/>

## ▶ FileInputStream객체 
파일을 Byte단위로 입력 처리를 할 수 있도록 해주는 객체

#### 1. File객체 생성
{% highlight ruby %}
File target = new File("D:\\datas", "a.txt");  
{% endhighlight %}

#### 2. File객체를 인자로 FileInputStream객체 생성
{% highlight ruby %}
FileInputStream fis = new FileInputStream(target);
또는
FileInputStream fis = new FileInputStream("파일경로");
{% endhighlight %}
생성자의 인자로 String형의 파일경로를 설정하게 되면, 1번단계인 File객체 생성을 생략가능하다.
<br/>=> FileInputStream객체를 생성하기 위해서는 FileNotFuondException을 예외처리 해야 한다. <br/>
( FileNotFoundException은 반드시 예외처리를 해야 하는 CheckedException )

#### ▶ FileInputStream객체 메서드
-  fis.available() 
: 현재 읽어낼 수 있는 크기를 반환하는 메서드로, 초기 값은 파일크기(target.length())와 같으며, 더 이상 읽어낼 자료가 없을 때는 0을 반환한다.<br/>
( 해당 메서드 또한 IOException을 예외처리 해야 한다. - CheckedException )
- int b = fis.read(); 
: 읽는 작업 ( 한번에 1바이트씩 읽음 ) => int형 아스키코드값을 반환
- int b = fis.read(byte[] t);
: 한 번에 byte배열 크기만큼 읽어 들임.<br/>
=> byte배열은 512~1024가 적정수준! ( 낮을수록 읽는 시간이 오래 걸림 )<br/>
=> byte배열로 읽어 들일 때 <font color="orange">실제 읽어들인 데이터는 해당 매개인자인 배열</font>로 들어가고, <font color="orange">반환되는 int값은 실제로 읽어 들인 칸의 수</font>!! 
- .close()  :  파일 사용이 끝났으면 닫아줘야 한다.

> 반복문을 통해서 fis.avilable()이 0이 될 때 까지 인자로 있는 byte[]배열에 계속해서 데이터를 읽어 들이고, 다른 배열에 해당 값을 계속해서 집어넣으면서 데이터를 받아오고, 마지막 작업에서 불필요한 데이터가 겹쳐 있기 때문에 실제 반환된 실제 읽어 들인 크기인 int만큼만 옮겨 담으면 된다.<br/>
=> 실질적으로 byte값이 읽거나 쓰여 지기 때문에 사람이 이해할 수 없는 데이터 값이지만, new String(byte[] t )로 스트링 객체의 매개변수를 읽어 들인 byte배열로 생성하면 파일의 내용을 알 수 있다.

{% highlight ruby %}
FileInputStream fis = null;
try {
	fis = new FileInputStream("C:\\Users\\gunbin\\Desktop\\fileinouttest.txt");
	while(true) {
        int a = fis.read();
		if(a == -1) break;
		System.out.println((char)a);
	}
} catch (FileNotFoundException e) {
    e.printStackTrace();
} catch (IOException e) {
	e.printStackTrace();
}finally {
	try {
        fis.close();
} catch (IOException e) {
    e.printStackTrace();
}
{% endhighlight %}

<br/>

## ▶ FileOutputStream 객체
파일의 출력 처리를 할 수 있도록 해주는 객체로, FileInputStream과 객체 생성 방법은 동일하다. 단, 출력이기 때문에 실제 <font color="orange">해당 파일이 존재하지 않는다면 FileOutputStream객체 생성 시 해당 파일을 자동으로 생성</font>해준다.

#### ▶ FileOutputSTream객체 메서드
- fos.write( int )  
: 1byte 출력
- fos.write(byte[] t )  
: byte배열로 출력
- fos.write(byte[] t ,int start ,int end );  
: byte배열의 start ~ end 까지만 출력<br/>
=> 나머지 배열의 무의미한 값들이 쓰기 되는 것을 방지!

> String형 데이터의 getBytes()메서드를 사용하면 byte형의 배열로 반환할 수 있다.

{% highlight ruby %}
try {
    FileOutputStream fos = new FileOutputStream("C:\\Users\\gunbin\\Desktop\\fostest.txt");
    String s = "hello java";
    fos.write(s.getBytes());
} catch (FileNotFoundException e) {
    e.printStackTrace();
} catch (IOException e) {
    e.printStackTrace();
}
{% endhighlight %}

<br/>

#### ▶ 파일의 byte 복사
cmd에서 copy기능은 해당 파일의 byte를 그대로 복사해서 확장자만 바꾼 형식이다. <br/>
즉 모든 파일은 byte단위로 구성되어 있기 때문에, File in/output stream을 통해 파일의 복사가 가능하다.<br/>
=> NetWork파일전송, 파일 수신도 같은 원리로 작동된다.

{% highlight ruby %}
try {
    FileInputStream fis = new FileInputStream("C:\\Users\\gunbin\\Desktop\\wall_e.jpeg");
	FileOutputStream fos = new FileOutputStream("C:\\Users\\gunbin\\Desktop\\copyimg.jpeg");
	byte[] data = new byte[10];
	while(true) {
	   int len = fis.read(data);
	   if(len == -1) break;
	   fos.write(data,0,len);
    }
} catch (FileNotFoundException e) {
    e.printStackTrace();
} catch (IOException e) {
    e.printStackTrace();
}
{% endhighlight %}

<br/>

# ◆ 입출력 보조 클래스
실질적으로 입출력 되는 byte값들을 사람이 이해할 수 있는 값들인 <font color="orange">int, double, String 등등으로 읽고 쓰기 위해</font> 사용하는 클래스 ( 바이트 입출력 서포트 )
<br/>

> 입출력 보조 클래스들은 생성 시 인자로 FileInputStream 또는 FileOutputStream객체를 받는다.<br/>
2차 클래스(보조 클래스)를 close 하면 1차 스트림도 close되기 때문에 FileOutputStream을 close할 필요가 없다.

<br/>

## ◆ Data(In/Out)putStream
Data(기본형 데이터)의 입출력을 보조해주는 객체이다.

#### ▶ DataOutputStream
- 객체생성: 
DataOutputStream dos = new DataOutputStream(FileOutputStream객체);  
- dos.writeInt(303);
: int형 데이터를 쓰기위한 메서드(4바이트로 저장된다)
- dos.writeDouble(4242.33);
: double형 데이터를 쓰기위한 메서드(8바이트)
- dos.writeUTF("모킹제이");
: String형 데이터를 쓰기위한 메서드(글자하나당 2바이트)
- dos.writeBoolean(true);
: boolean형 데이터를 쓰기위한 메서드(1바이트)
- dos.close()
  
<br/>
  
#### ▶ DataInputStream 객체
- 객체생성
: DataInputStream dis = new DataInputStream(fis);
- int n = dis.readInt(); 
: 4바이트를 읽어서 int로 변환
- Double d = dis.readDouble();
: 8바이트를 읽어서 double로 변환
- String s = dis.readUTF();
: 글자당 2바이트씩 읽어서 String반환 
- Boolean b = dis.readBoolean();
: 1바이트로 읽어서 boolean으로 반환

> DataIn(Out)putStream객체를 이용하여 파일을 읽을 때 저장했던 데이터형의 순서에 맞게 불러와야한다.
따라서 저장했던 데이터의 순서를 알고 있을 경우에만 불러올 수 있다. 이를 어길 시 데이터의 손실이 생길 수 있다. 

<br/>

## ◆ Object(In/Out)putStream
Object를 입출력하기 위한 보조클래스로 Obejct로 관리하기 때문에 Data(In/Out)putStream보다 많은 데이터를 쉽게 처리할 수 있다.<br/>
> 단 모든 클래스들이 파일 입/출력을 할 수 있는 것은 아니고, byte로 변환이 가능한 Serializable(직렬화)를 implements한 클래스들만 가능하다.<br/>
( 기본적으로 컬렉션, 배열, String, Wrapper 등등 자주쓰이는 객체들은 모두 직렬화가 구현되어 있다.)

<br/>

#### ▶ ObjectOutputStream 객체
- 객체생성
: ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream(dest));
<br/>=> 객체가 생성됨과 동시에 파일이 생성될 때, 파일에 4byte가 미리 만들어진다.<br/>
( 읽을 때 해당 파일에 해당 4byte값이 변경되거나 없으면 Object로 읽기가 불가능하다 )
- oos.writeObject(Object);
: 파일에 객체를 바이트화 시켜서 출력시킬 수 있다.

<br/>

#### ▶ ObjectInputStream 객체
- 객체생성
: ObjectInputStream ois = new ObjectInputStream(new FileInputStream(src));
- int[] o = (int[]) ois.readObject();
: 이런 식으로 읽어 들인 Object를 다운 캐스팅하여 사용한다.

<br/>

#### ▶ 직렬화 ( Serialization ) 
객체를 byte로 변환 시키는 과정 ( writeObject() )

- 역 직렬화 
: byte데이터를 객체로 변환시키는 과정( readObject() )
읽거나 쓰고자 하는 객체 클래스 안에 직렬화가 되어있지 않은 객체가 있어도 writeObject() 또는 readObject()를 할 수 없다. ( 단 Serializable을 구현한 클래스 계열의 객체는 가능 )

<br/>

# ◆ 자동 변환 입출력 클래스

## ▶  OutPutStreamWriter / InputStreamReader
위에 입출력 보조클래스들로 입/출력 했던 내용들을 실제 열어보면 사람이 이해할 수 있는 문자가 아니다. 이는 자바의 문자 byte값과 파일의 문자byte값이 다르기 때문이다.

>따라서 <font color="orange">실제로 사람이 이해할 수 있는 내용으로 파일을 읽고 쓰기위해서는 이를 변환해 주는 OutputStreamWriter/ InputStreamReader 객체가 필요</font>하다.

- 객체 생성
{% highlight ruby %}
OutputStreamWriter osw 
= new OutputStreamWriter(new FileOutputStream(dest), "UTF-8");
- InputStreamReader isr 
= new InputStreamReader(new FileInputStream(dest), "unicode");
{% endhighlight %}

=> OutputStreamWriter / InputStreamReader 도 
마찬가지로 File객체와 fileOut/InputStream 객체가 있어야한다.<br/>
=> 생성 시 <font color="orange">두 번째 매개인자로 해당 파일의 캐릭터셋과 일치하는 캐릭터셋을 지정</font>해줘야 컴퓨터가 인식하고 변조해 줄 수 있다.
- osw.write(String형 또는 char형)
: 자바파일에서의 글자가 그대로 메모장에 적힌다.
- isr.read()
: 해당 문자를 int형으로 반환한다.  
이 int형으로 반환된 수를 char형으로 캐스팅하면 해당 문자를 볼 수 있다.
읽을 내용이 없으면 -1을 반환

<br/>

## ◆ BufferedReader, BufferedWriter
문자를 처리 할 때, 라인 단위 작업을 지원하기 위해서 만들어진 클래스 

#### 객체생성
{% highlight ruby %}
  - BufferedWriter bw 
  = new BufferedWriter(new OutputStreamWriter(new FileOutputStream(d)));
  - BufferedReader br 
  = new BufferedReader(new InputStreamReader(new FileInputStream(d)));
{% endhighlight %}
Buffered(Reader/Writer)객체를 생성할 때 인자로 (Out/In)putStream(Writer/Reader)객체로 하기 때문에 최종적으로 세개의 객체를 필요로 하는것과 같다.

#### 쓰기  
- bw.newLine();  
: 줄 바꿈 ( BufferedWriter를 쓰는 이유 )<br/>
=> 또는 write할때 \r\n 을 같이 써줘야 줄 바꿈 처리가 된다.
- bw.write(String s ) 
: String형 내용입력<br/>
=> String형이 아닌 기본형 데이터들은 String으로 변환해줘야 한다. <br/>
( toString 또는 valueOf 또는 + " " )

#### 읽기
- br.readLine()  
: 줄 바꿈이 있기 전까지 String형으로 받아옴<br/>
=> 읽어올 데이터가 없으면 null 반환

#### 콘솔입력 읽기
{% highlight ruby %}
BufferedReader br = new BufferedReader(new InputStreamReader(System.in));  
{% endhighlight %}
파일객체 또는 경로 대신 System.in을 쓰게 되면 콘솔을 이용하여 입출력을 하겠다는 의미이다. 따라서 System.in을 인자로 생성하게 될 경우 콘솔창에서 입출력을 제어할 수 있다.

<br/>

# ◆ 출력 전용 객체
#### ▶ PrintStream vs PrintWriter ( File 또는 FileOutputStream을 인자로 )
{% highlight ruby %}
PrintWriter pw = new PrintWriter(new FileOutputStream(f));
PrintStream ps = new PrintStream(new FileOutputStream(f));
{% endhighlight %}
=> 매개변수로 File, FileOutputStream 모두 가능하다.<br/>
- System.out.println()메서드를 이용하듯이 <font color="orange">.print(), .println()등의 기능이 가능</font>해지기 때문에 출력이 쉬워진다.

- 차이점 
: PrintStream은 출력이 있을 때 마다 Flush가 일어난다. <br/>
특수한 경우에 사용 PrintWriter은 적당량이 차있거나 close() 될 때 Flush가 일어난다. 
- Flush 
: 문자열 출력은 Flush가 되어야만 출력이 됨 <br/>
( 문자열들은 모아놨다가 적당량(8kb) 모였을 때 한번씩 flush 되는 구조 )<br/>
=> .close(); 가 호출될 때 Flush가 일어나게 되어 있음.<br/>
=> .flush(); 강제출력<br/>

# ◆ 입력 전용 객체
#### ▶ Scanner (java.util)  : 입력을 편하게
- Scanner c = new Scanner(new FileInputStream("d:\\datas\\ddd.txt"));
: 파일의 내용을 .next() 로 읽어 들일 수 있게 된다. ( 디폴트 단위는 공백 )
- c.useDelimiter(",");  
: next로 읽어 들일 때 구분자를 설정
- .nextInt() 
: Integer.parseInt(next()); 로 만들어 둔 것.
- Scanner c = new Scanner(System.in);
: 콘솔로 입력받을 수 있게 됨.







<br/>