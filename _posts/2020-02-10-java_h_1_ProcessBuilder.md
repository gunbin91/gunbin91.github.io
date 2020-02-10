---
layout: post
title: "18. 커맨드라인 사용하기 ProcessBuilder"
tags: [ java, java api, processbuilder ]
date: 2020-02-10
categories: [ java ]
---

<p align="center">
    JAVA단에서 명령프롬프트에 접근하여 결과스트링을 받아오는 방법에 대해 알아보자.
</p><br/>

## ◆ ProcessBuilder
ProcessBuilder객체를 사용하여 Linux 또는 Window의 커맨드라인의 커맨드입력을 실행할 수 있다.
{% highlight ruby %}
// 운영체제에 따라 첫 실행 명령어가 달라진다.
public ProcessBuilder inputCommand(String cmd) {
	builder = new ProcessBuilder();
	try {
		if (System.getProperty("os.name").indexOf("Windows") > -1) {
            builder.command("cmd.exe", "/c", cmd);
            builder.directory(new File("/"));
		} else {
            builder.command("sh", "-c", cmd);
            builder.directory(new File("/usr/local/bin/"));
		}
	} catch (Exception e) {
		e.printStackTrace();
		}
	return builder;
}
{% endhighlight %}
- command("커맨드") 
: 커맨드 입력메서드
- directory(new File("파일경로")) 
: 해당 커맨드를 실행할 경로

<br/>

## 커맨드 결과 읽기
ProcessBuilder를 통해 start()(커맨드실행)호출 시 Process객체를 반환하고,
해당 객체의 getInputStream()을 통해 커맨드 결괄르 읽어들일 수 있다.
{% highlight ruby %}
public List<String> execCommandList(ProcessBuilder builder) {
	try {
		String line = null;
		ArrayList<String> list = new ArrayList();

		process = builder.start();
		bufferedReader = new BufferedReader(new InputStreamReader(process.getInputStream()));
			
		if(bufferedReader != null || !bufferedReader.equals("")){
            list.add("	[ProcessBuilder Success] : ");
            while ((line = bufferedReader.readLine()) != null) {
                list.add("		" + line);
            }
		}

		bufferedReader = new BufferedReader(new InputStreamReader(process.getErrorStream()));
		
		if(bufferedReader != null || !bufferedReader.equals("")){
            list.add("	[ProcessBuilder Error] : ");
            while ((line = bufferedReader.readLine()) != null) {
                list.add("		" + line);
            }
		}

		return list;
	} catch (Exception e) {
		e.printStackTrace();
	}
	return null;
}
{% endhighlight %}
- ProcuessBuilder.start()
: 커맨드 실행
- Process.getInputStream()
: 커맨드 결과 반환
- Process.getErrorStream()
: 커맨드 에러 반환

> ProcessBuilder가 반환하는 결과에 에러가 포함되어 있지 않기 때문에 getErrorStream을 따로 생성하여 에러로그를 출력 할 수 있도록 설계해야한다.

## ProcessBuilder의 권한
리눅스의 경우 사용자가 여러명이기 때문에 ProcessBuilder를 통해 커맨드를 실행할 때,
해당 권한은 <font color="orange">WAS 또는 class를 실행시킨 사용자의 권한으로 실행</font>된다.
<br/>
따라서 이점을 유의하여 설계해야한다.




<br/>