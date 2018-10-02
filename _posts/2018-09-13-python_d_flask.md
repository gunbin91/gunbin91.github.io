---
layout: post
title: "Flask 웹 프레임워크"
tags: [ python, flask, 파이썬, 플라스크 ]
date: 2018-09-13
categories: [ python ]
---

<p align="center">
    Flask는 파이썬으로 웹 개발을 하기 위한 프레임워크이며, 장고보다 가볍다는 장점이 있다.
</p><br/>

# Flask
파이썬 기반 마이크로 프레임워크<br/>

- 마이크로 프레임워크란? 
: 프레임워크의 핵심기능만 유지하고, 다른 기능들은
확장에 기준을 둔 가벼운 프레임워크 따라서, 빠른 웹 개발이 가능하다

# Flask 객체생성
Flask를 사용하기 위해서는 플라스크 객체생성이 필요하다. 
{% highlight ruby %}
from flask import Flask
app = Flask (__name__)

if __name__ == "__main__":
    app.run(debug=True)
{% endhighlight %}

- 위와 같이 코드를 작성한 후 콘솔에서 <font color="orange">'python 파일명.py'</font>를 실행시키면, <br/>
플라스크 객체를 생성한 후, 해당객체의 run()메서드를 실행할 때 <font color="orange">5000번 포트로 플라스크 자체 서버가 구동</font>된다. 아래와 같이 뜨게되면 서버구동에 성공한 것이다.
<img src="{{ site.baseurl }}/assets/post_img/flask_run.JPG" height="250px" style="padding:0;margin:0;">

<br/><br/>

# Flask실행
위와 같이 플라스크를 실행하는 구문은 플라스크객체의 run()메서드 이다.<br/>
보통은 가장 최하단에 놓이게 된다.

{% highlight ruby %}
if __name__ == "__main__":
	app.run(debug=True)
{% endhighlight %}
<br/><br/>

# Flask URL처리
웹 페이지의 접속경로에 따른 함수를 정의할 때 <font color="orange">'@app.route("경로")'</font>어노테이션을 함수위에 적고 페이지 이동 전 처리할 작업들을 코드로 작성한다. 기본적으로 해당 함수에서 <font color="orange">문자열 리턴시 html문법으로 브라우저에 출력</font>하게 된다.
{% highlight ruby%}
@app.route('/')
def index(): 
    return "<h1> Hello Python ! </h1>"
{% endhighlight %}

<img src="{{ site.baseurl }}/assets/post_img/flask_index.JPG" height="250px" style="padding:0;margin:0;">
<br/><br/>


# 동적 URL
접근 url을 동적으로 지정할 수도 있다. 동적으로 url을 지정할 경우 <font color="orange">'&lt; 변수 >' </font>를 통해 해당 경로부분에 대해서는 <font color="deeppink">어떤 문자열을 입력하든 해당 함수로 이동</font>하게 된다.<br/>
단, 꼭 함수의 인자로 <font color="orange">해당 경로 문자열을 받을 수 있는 매개인자를 정의</font>해 두어야한다.<br/>
{% highlight ruby %}
@app.route('/nos/<code>')
def item(code):
    return "<h1> %s </h1>" % code
{% endhighlight %}
<img src="{{ site.baseurl }}/assets/post_img/flask_dynamic.JPG" height="250px" style="padding:0;margin:0;">
<br/><br/>

#### ▶ 동적URL 자동 파싱
동적 URL을 자동으로 파싱해서 가져오고 싶을 경우 <font color="orange">&lt;int:변수>, &lt;float:변수> </font>등과 같이 처리해서 가져오면 된다.<br/>
- &nbsp;<font color="orange">&lt;path:변수></font>의 경우에는 문자열+"/" 등으로 가져오게 된다.
<br/><br/>

# query String 가져오기
query String은 경로뒤에 따라오는 파라미터 인자값들을 의미하며 form태그를 통해 보낼 수 있다.<br/>
form태그를 통해 데이터를 보내게 되면 <font color="orange">'경로?name=value'</font>의 형식으로 경로가 이동되며, 직접 주소창에 입력해도 무방하다.<br/><br/>
해당 파라미터를 함수내부로 가져오기 위해서는 우선 <font color="orange">flask의 request모듈이 필요</font>하다.<br/>
&nbsp;<font color="orange">request.form[name]</font> 또는 <font color="orange">request.values[name]</font>을 사용하여 queryString의 파라미터를 가져올 수 있다.
{% highlight ruby %}
form flask import request

@app.route("/msg")
def reverse():
    values = request.values
    message = values["message"]
    return "".join(reversed(message))
{% endhighlight %}

>단, 주의해야 할점은 url주소창에 노출되는 파라미터의 경우는 form의 method방식이 GET일 경우에만 가능하며, form을 통해 보내지 않은 데이터는 request.form으로 불러올 수 없다.
<br/>

<img src="{{ site.baseurl }}/assets/post_img/flask_querystring.JPG" height="250px" style="padding:0;margin:0;">

<br/><br/>

- form의 <font color="orange">method방식 확인은 request.method</font>를 사용하여 확인이 가능하다. <br/>
따라서 이것을 이용하여 같은경로의 메서드 방식에 따라 다른 화면을 보여줄 수도 있다.
{% highlight ruby %}
@app.route("/msg",  methods=['GET','POST'])
def reverse():
    if request.method == 'GET' :
        return "<form action='/msg' method='POST'><input type='text' name='message'></form>"
    else :
        form = request.form
        message = form["message"]
        return "".join(reversed(message))
{% endhighlight %}
> 단, 기본적으로 flask는 post방식을 차단하기 때문에, <font color="orange">@app.route("/msg",  methods=['GET','POST'])</font>를 이용하여 <font color="orange">메서드 허용범위를 지정</font>해 주어야 한다.

<br/><br/>

# templates구현
파이썬코드에서 리턴값으로 일일히 HTML태그를 찍어내는 것은 코드가 매우 지저분해고, 어렵기 때문에 Flask에서는<font color="deeppink"> Jinja라는 템플릿엔진</font>을 기본적으로 
지원해준다. 이 템플릿 엔진을 사용하기 위해서는 flask모듈의 <font color="orange">render_template(html파일명, 보낼인자)가 필요</font>하다.
{% highlight ruby %}
from flask import render_template

@app.route('/hello/<name>')
def hello(name):
    msg = request.values["msg"]
    return render_template('test.html', name=name, msg=msg)
{% endhighlight %}
test.html
{% highlight ruby %}
...
<body>
    <h2>NAME = {{name}}</h2>
    <h2>MSG = {{msg}}</h2>
</body>
...
{% endhighlight %}

 <img src="{{ site.baseurl }}/assets/post_img/temp.JPG" height="250px" style="padding:0;margin:0;">
 
 - 위와 같이 render_template()로 반환하게 될 경우, 해당 html파일을 브라우저로 보여주고 인자값을 전달할 수도 있다. ( 해당 html파일에서 인자값을 불러오는 방법에 대해서는 Jinja문법에서 살펴보자 )
<br/><br/> 

### ▶ 템플릿파일 경로처리
render_template()에서 html파일을 불러올 때, 해당 <font color="deeppink">html파일은 'templates'라는 디렉터리 안에서 찾게된다.</font> 따라서 반드시 templates디렉터리가 있어야 하며,<font color="deeppink"> html파일또한 templates내부에 존재</font> 해야한다.<br/>
( 즉, templates디렉터리가 해당 함수에서의 /가 되는것이다. )
<br/><br/>

# 세션제어
Flask에서 세션을 제어 하기위해 flask모듈의 <font color="deeppink">session객체가 필요</font>하다. 또한 flask에서 <font color="deeppink">세션을 제어하기 위해서는 비밀키를 미리 설정</font>해 두어야 한다.

### ▶ 비밀키 설정 
{% highlight ruby %}
app.secret_key = "사용자정의"
{% endhighlight %}
<br/>

### ▶ 세션에 키값 저장
{% highlight ruby %}
session['username'] = request.form['username']
{% endhighlight %}
<br/>

### ▶ 세션값 제거
{% highlight ruby %}
session.pop('username', None)
{% endhighlight %}
<br/>

### ▶ 세션키 가져오기
{% highlight ruby %}
session.get('logged')
{% endhighlight %}
<br/>

# 리다이렉트( Redirect )
리다이렉트는 다른 경로로 이동시켜주는 기능으로 flask모듈의 <font color="orange">redirect</font>가 필요하며, 함수의 경로를 찾아내기 위해 url_for()를 사용하는데, 이또한 flask모듈의 <font color="orange">url_for</font>가 필요하다.

- &nbsp;<font color="orange">'return redirect('경로')'</font>를 이용하여 해당 경로로 이동시킬 수 있으며, <font color="orange">'url_for('함수명',인자)</font>을 이용하여 해당 함수의 경로를 추출해낼 수 있다.
{% highlight ruby %}
@app.route('/login', methods=['GET', 'POST'])
def login():
    if request.method == 'POST':
        session['username'] = request.form['username'] 
        return redirect(url_for('login_index')) 
    return '''
        <form action="" method="post">
            <p><input type=text name=username>
            <p><input type=submit value=Login>
        </form>
    '''
{% endhighlight %}
<br/><br/>

### ▶ 리다이렉트 시 데이터 넘겨주기
리다이렉트 시 데이터를 넘겨줄 때 <font color="orange">url_for('함수명',인자)</font>를 통해 인자를 넘겨주면, 해당 인자가 url경로의 queryString으로 붙게된다.
{% highlight ruby %}
redirect(url_for('member',page='login.html',state=1))
=> member경로?page=login.html&state=1 가 반환된다.
{% endhighlight %}
- 이렇게 보내진 인자는 member()함수에서 <font color="orange">'request.values'</font>로 뽑아낼 수 있다.
<br/><br/>

# 그 외

## html로 데이터 넘겨주기
return render_template('test.html', re=result)의 형식으로 html파일로 데이터를 넘겨줄 수 있다.
<br/><br/>

## css파일과 js파일의 경로
flask에서 html파일을 template디렉토리 아래에서 찾게되듯이,<font color="deeppink">css, js파일 또한 지정된 'static'라는 디렉토리</font> 아래에서 찾게 된다.<br/>
따라서 static디렉토리 내부에 css, js파일을 나누어 배치하고,
html파일에서 해당 파일들을 불러올 때는 <font color="orange">url_for('static', filename='css/base.css')</font> 등으로 불러올 수 있다.

## 캐시 새로고침
불러온 css파일의 경우 캐시에 저장되어 보여주기 때문에,<br/> 새로고침만으로 수정된 결과를 바로 확인할 수 없다.
따라서 캐시를 초기화 시켜주어야 하는데<br/><font color="orange">'ctrl + shift + r'</font>단축키를 이용하면 캐시초기화및 새로고침을 동시에 해줄 수 있다.

## DB 쿼리실행
{% highlight ruby %}
   try:
        with connection.cursor() as cursor:
            query = '''
            SELECT * FROM dbo.Channel_ID where CHANNEL_ID=%s
            '''
            cursor.execute(query,(cid))
            row=cursor.fetchall()
    except _mssql.MssqlDatabaseException as e:
        application.logger.error(e)
    except Exception as e:
        application.logger.error(e)
{% endhighlight %}
- 쿼리문에 %s를 삽입하여 execute()메서드를 실행할 때 인자로 데이터를 세팅할 수 있다.
- execute(query, (cid))를 통해 쿼리 실행 시 데이터를 넣을 수 있다.
- 또한 fetchone()이 아닌 fetchall()을 실행하 시 한번에 모든 데이터를 가져올 수 있다.
<br/><br/>

## html에서 쿼리 순회
DB에서 fetchall()을 통해 받아오는 데이터는 ImmutableMultiDict형으로 for k,v in a.items() : 로 순회할 수 있다.
{% highlight ruby %}
{% raw %}
{% for key, value in re.items() %}
            <tr>
               <th> {{ key }} </th>
               <td> {{ value }} </td>
            </tr>
{% endfor %}
{% endraw %}
{% endhighlight %}


<br/>