---
layout: post
title: "File 업로드 처리"
tags: [ python, python file, multipart ]
date: 2018-09-19
categories: [ python ]
---

<p align="center">
    파일을 불러오기 위해서는 조금 다른 명렁어를 입력해야 하며,<br/> 파일 처리를 위해 html폼에서 enctype을 변경해 주어야 한다.
</p><br/>

# html폼의 enctype변경
기본적으로 폼태그의 enctype을 지정하지 않을 시에는 디폴트값인 'application/x-www-form-urlencoded'로 간주되기 때문에 파일을 전송하고자 할 경우 꼭 <font color="orange">enctype을 multipart/form-data</font>로 지정해 주어야 한다.<br/> 또한 GET방식으로는 불러올 수 없기 때문에 <font color="orange">method또한 POST로 설정</font>해 주어야 한다.
<br/><br/>

# request.files로 파일 불러오기
기존에 html폼에서 보낸 데이터를 불러올 때는 request.values 또는 request.form을 사용하였지만, 파일을 불러올 때는 <font color="orange">request.files['name']</font>를 사용하여 불러온다.<br/> 이는 파일명이 담겨있는 스트링객체가 아닌 파일객체이다.
> 파일명을 불러오고자 할 경우 '파일.filename'을 사용하면 된다.

<br/><br/>

# file.save(경로)
파일을 실제로 서버에 <font color="orange">업로드</font> 즉 저장시키기 위해서는 <font color="orange">파일객체.save("경로","파일명")</font>를 사용한다. 
<br/><br/>

# 파일경로로 이동
파일이 있는 경로를 url에 입력하게 되면 해당 이미지를 볼 수 있다. (즉, '서버ip/파일경로/파일명' )이를 플라스크를 거쳐 경로를 변경하고 싶을 때는 <font color="orange">return send_form_directory("경로","파일명")</font>을 사용하면 해당 메서드의 @app.route("경로")에 접근했을 경우 해당 파일을 웹 상에 띄워주게 된다.
<br/><br/>

# 파일업로드 예제
{% highlight ruby %}
import os
from flask import Flask, request, redirect, url_for
from flask import send_from_directory
from werkzeug.utils import secure_filename

UPLOAD_FOLDER = ''
app.config['UPLOAD_FOLDER'] = UPLOAD_FOLDER
ALLOWED_EXTENSIONS = set(['txt', 'pdf', 'png', 'jpg', 'jpeg', 'gif'])

@app.route('/', methods=['GET', 'POST'])
def upload_file():
    if request.method == 'POST':
        # 파일이없다
        if 'file' not in request.files:
            flash('No file part')
            return redirect(request.url)
        
        # 파일네임이없다 ( .filename )
        if file.filename == '':
            flash('No selected file')
            return redirect(request.url)
        
        # 파일 가져오기 ( request.files['네임'] )
        file = request.files['file']
            
        if file and allowed_file(file.filename):
            filename = secure_filename(file.filename)
            # 업로드 ( .save(경로) )
            file.save(os.path.join(app.config['UPLOAD_FOLDER'], filename))
            return redirect(url_for('uploaded_file', filename=filename))
            
# 파일이 허락된 형식인지검사
def allowed_file(filename):
    return '.' in filename and \
           filename.rsplit('.', 1)[1].lower() in ALLOWED_EXTENSIONS

# 파일이 있는 경로로 이동시킴
@app.route('/uploads/<filename>')
def uploaded_file(filename):
    return send_from_directory(app.config['UPLOAD_FOLDER'], filename)
{% endhighlight %}


<br/>