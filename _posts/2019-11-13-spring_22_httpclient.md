---
layout: post
title: "22. 데이터 주고받기 - HttpClient"
tags: [ spring, httpclient ]
date: 2019-11-13
categories: [ spring ]
---

<p align="center">
    클라이언트의 접근없이도 서버 자체내에서 컨트롤러로의 요청을 처리할 수 있는 방법에 대해 알아보자.
</p><br/>

## ◆ org.apache.commons.httpclient
백단에서 네트워크 데이터를 주고받을 수 있도록 get, post요청과 응답을 지원해준다.

<br/>

### ▶ MAVEN
https://mvnrepository.com/artifact/commons-httpclient/commons-httpclient/3.1
{% highlight ruby %}
<!-- https://mvnrepository.com/artifact/commons-httpclient/commons-httpclient -->
<dependency>
    <groupId>commons-httpclient</groupId>
    <artifactId>commons-httpclient</artifactId>
    <version>3.1</version>
</dependency>
{% endhighlight %}

<br/>

### ▶ 응답컨트롤러 ex
{% highlight ruby %}
@ResponseBody
@RequestMapping(path="/send", method=RequestMethod.POST)
public String sendPost(@RequestParam Map paramMap){
	System.out.println("[--응답 호출 S--]");
	for(Object val: paramMap.keySet()){
		System.out.println("키: " + val + " / 값 : " + paramMap.get(val));
	}
	System.out.println("[--응답 호출 E--]");
	
	return "return string data ..!";
}
{% endhighlight %}

<br/>

### ▶ 요청스케줄 ex
HttpClient객체를 생성하고 인자를 PostMethod객체로 하는 <font color="orange">executeMethod()메서드를 호출하면 요청이 전달</font>된다. (Get방식의 요청은 GetMethod)<br/>

- 파라미터 설정방법
: 1. NameValuePair객체를 통하여 설정 후 PostMethod객체의 <font color="orange">setRequestBody메서드의 인자로 NameValuePair배열</font>을 넘겨준다.
2. PostMethod객체의 <font color="orange">addParameter("key","value")메서드를 통해 설정</font>
{% highlight ruby %}
@Scheduled(cron="00 05,10,15,20,25,30,35,40,45,50 * * * * ")
public void test(){
	PostMethod post = new PostMethod("http://127.0.0.1:8181/send");
	// 파라미터설정 1
	NameValuePair sitecd = new NameValuePair("A", "1");
	NameValuePair langcd = new NameValuePair("B", "2");
	post.setRequestBody(new NameValuePair[]{sitecd, langcd});
        
	//파라미터 설정 2
	post.addParameter("C","3");
        
	try {
		HttpClient httpClient = new HttpClient();
		int returnCode = httpClient.executeMethod(post);
		System.out.println("리턴코드: " + returnCode);
		System.out.println("에러코드: " + HttpStatus.SC_NOT_IMPLEMENTED);
		System.out.println("리스폰스바디: " + post.getResponseBodyAsString());
	} catch (IOException ioe) {
		ioe.printStackTrace();
	} finally {
		post.releaseConnection();
	}        
        
	return "test.jsp";
}

// sysout 결과
[--응답 호출 S--]
키: A / 값 : 1
키: B / 값 : 2
키: C / 값 : 3
[--응답 호출 E--]
리턴코드: 200
에러코드: 501
리스폰스바디: return string data ..!
{% endhighlight %}



<br/>