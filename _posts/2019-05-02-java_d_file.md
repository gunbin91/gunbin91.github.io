---
layout: post
title: "13. 파일객체"
tags: [ java, file ]
date: 2019-05-02
categories: [ java ]
---

<p align="center">
    자바에서는 외부 파일을 제어할 수 있는 File이라는 객체도 가지고 있다. <br/>파일을 제어하기 위한 객체인 File객체에 대해 알아보자.
</p><br/>

# ◆ File객체
Java에서 파일들을 제어하기 위해 파일들과 연결해주는 객체

#### ▶ File 객체 생성 
파일객체를 생성할 때, 사용할 파일의 경로와 파일명을 String인자로 써 주어야 한다.<br/>
단, 파일명만 적을 시 해당 파일의 경로(부모)는 해당 자바프로젝트의 경로(상대경로)가 된다.<br/>
( 파일객체는 디렉터리가 될 수도 있고, 꼭 존재하지 않아도 된다.)
<br/>

- File(String)
: String인자가 하나인 File객체 생성자는 해당 파일의 풀 경로를 적어 주어야 한다.
{% highlight ruby %}
File f1 = new File("D:\\17_10_Web_Jogunbin\\filetest"); // 디렉터리파일
File f2 = new File("D:\\17_10_Web_Jogunbin\\filetest\\test.txt"); // 텍스트파일
{% endhighlight %}

<br/>

- File(String parent, String child)
: String인자가 두 개인 File객체 생성자는 첫 번째 인자로 파일의 경로(부모), 두 번째 인자로 파일명을 적어 주어야 한다.
{% highlight ruby %}
File f3 = new File("D:\\17_10_Web_Jogunbin\\filetest\\", "test.txt"); 
{% endhighlight %}

<br/>

- File(File parent, String child)
: File객체의 첫 번째 인자로 또 다른 File객체를 받을 때는 인자로 들어온 파일은 디렉터리이어야 하고, 해당 인자로 들어온 File객체가 부모(경로)가 된다.
 {% highlight ruby %}
 File f1 = new File("D:\\17_10_Web_Jogunbin\\filetest"); // 디렉터리파일
 %}File f4 = new File(f1, "JAVA"); 
 {% endhighlight %}
  
<br/>

#### ▶ File 메서드
- .getAbsolutePath(); 
: 파일의 절대경로 String 반환
- .getName();  
: 파일의 이름 String  반환
- .exists(); 
: 파일의 존재여부 boolean 반환
- .isDirectory();  
: 해당 파일이 디렉터리인지 boolean 반환
- .isFile();  
: 해당 파일이 파일형태인지 boolean 반환
- .isHidden();  
: 해당 파일이 숨김 파일인지 boolean 반환
- .length();  
: long형(단위 byte) 반환<br/>
=> 파일이라면 파일크기, 디렉터리라면 소속파일 총 크기(크게 의미 없음)
- .lastModified(); 
: 최종 수정 일자(1970~)를 long형으로 반환<br/>
=> new Date(t.lastModified());로 볼 수 있다.
- .list(); 
:  디렉터리 안에 있는 모든 파일목록을 String[] 로 반환<br/>
=> 파일변수가 디렉터리일 때만 가능. ( 단, 디렉터리가 비어있으면 불가능 )
- .listFiles(); 
: 디렉터리 안에 있는 모든 파일목록을 File[] 로 반환
- .mkdir(); 
: 파일변수에 적힌 경로와 이름으로 디렉터리를 생성<br/>
=> 실패ex) 이미 있거나, 파일 안에 디렉터리를 생성하거나, 부모디렉터리가 없는 경우.
- .createNewFile();  
: 디렉터리가 아닌 파일로 생성
- .renameto(파일변수) 
: 파일 이름 변경<br/>
=> 실패ex) 원본대상이 없거나, 바꾸고자 하는 이름의 파일이 있는 경우
- .delete()  
: 파일삭제<br/>
=> 실패ex) 타겟이 없거나, 디렉터리에 소속된 애들이 있는 경우

<br/>

#### ▶ 파일 선택 인터페이스(JFileChooser)
파일객체의 생성을 유저인터페이스로 선택할 수도 있다.<br/>

#### 1. JFileChooser 객체 생성
JFileChooser f = new JFileChooser();
#### 2. showOpenDialog()메서드로 파일 선택 창 띄우기
f.showOpenDialog(null);
#### 3. File객체 반환







<br/>