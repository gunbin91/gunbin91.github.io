---
layout: post
title: "10. 파이썬 표준 라이브러리"
tags: [ python, python library ]
date: 2018-09-12
categories: [ python ]
---

<p align="center">
    파이썬을 설치할 때 함께 설치되는 유용한 모듈인 표준 라이브러리에 대해 알아보자.
</p><br/>

# sys
시스템의 기능을 다루는 함수들로 이루어진 모듈<br/>

- sys.version_info
: 파이썬 버전에 대한 정보를 출력
<br/><br/>

- sys.version_info.major
: 파이썬 메이저버전을 반환
<br/><br/>

- sys.stdout.flush()
: 현재 읽어들인 문자열을 바로바로 콘솔로 출력
<br/><br/>

- sys.argv
: 콘솔에서 .py를 실행했을 때 받는 인자 값
<br/><br/>

- sys.exit()
: 강제종료
<br/><br/>

# os

- os.path.exists("경로")
: 해당 경로가 존재하는지 안하는지 True/False 반환
<br/><br/>

- os.sep
: 운영체제마다 디렉토리 구분자가 다른데( Linux/Unix = '/', 윈도우='/ \', Max = ':' )<br/>
이를 구분하지 않고 범용으로 쓸 수 있도록 디렉토리 구분자를 자동으로 처리해주는 변수
<br/><br/>

- zip -r 경로1 경로2 ... => ( 시스템 명령어 )
: 경로1인 zip파일명으로 경로2를 압축<br/>
( -r 옵션은 해당 파일의 하위 폴더까지 모두 포함하겠다는 의미 )
<br/><br/>

- os.system("명령어")
: cmd에서 쓰이는 시스템 명령어를 실행할 수 있는 메서드 수행이 성공적으로 실행된 경우에만 0을 반환<br/> => 하게 되면 콘솔창으로 해당 명령문에 대한 진행 사항이 출력됨
<br/><br/>

- os.mkdir("경로")
: 해당 경로로 디렉토리를 생성
<br/><br/>

- os.getcwd()
: 현재 디렉터리위치를 문자열로 반환
<br/><br/>

- os.popen(“명령어”)
: 콘솔창의 시스템 명령어를 실행하고 결과값을 읽기 모드 파일 객체로 리턴<br/>
ex ) f = os.popen(“dir”)<br/>
print(f.read())
<br/><br/>

- os.getenv("HOMEDRIVE")
: C드라이브 경로 반환
<br/><br/>

os.getenv("HOMEPATH")
: 사용자 파일이름 반환
<br/><br/>

# logging
프로그램 실행 중 변수 또는 메시지를 로그파일에 저장해 둘 수 있게 도와주는 모듈<br/><br/>

#### 로그파일 형식지정
{% highlight ruby %}
logging.basicConfig(
    level=logging.DEBUG,
    format='%(asctime)s : %(levelname)s : %(message)s',
    filename = logging_file,
    filemode = 'w',
)
{% endhighlight %}
를 통하여 로그 파일의 기록 형식을 지정할 수 있는데,
이 중 format속성의<br/>
(asctime)s 는 로그를 남긴 시간을 기록하는 곳이고,<br/>
(levelname)s 는 로그 파일의 어떤 정보 인지를 표시하는 곳이고,<br/>
(message)s 는 로그 파일에 남긴 기록이다.<br/>
filename속성은 로그파일을 남길 파일 객체이며,<br/>
filemode 는 모드를 선택하는 속성이다.<br/>
<br/>
{% highlight ruby %}
logging.debug("Start of the program")
logging.info("Doing something")
logging.warning("Dying now")
{% endhighlight %}
라고 코드를 작성하여 디버그 할 경우 해당 로그파일에는
~~~
2018-06-11 14:11:51,326 : DEBUG : Start of the program
2018-06-11 14:11:51,326 : INFO : Doing something
2018-06-11 14:11:51,326 : WARNING : Dying now
~~~
라는 기록이 남게 된다.

# time
시간에 관한 정보를 제어할 수 있게 해주는 모듈<br/>

- time.strftime("%Y%m%d%H%M%S") 
: 현재 날짜와 시간을 문자열로 반환<br/>
=> %Y = 네자리 연도, %m = 두 자리의 달
<br/><br/>

- time.sleep(숫자)
: 숫자(초단위)만큼 프로그램 실행상태를 일시정지
<br/><br/>

- time.time()
: 현재 시간을 실수 형태로 리턴
<br/><br/>

- time.localtime( time.time() )
: time.time()이 반환하는 실수 값을 년,월,일,시,분초 형태로 바꾸어 주는 함수<br/> 즉, 실수를 time형으로 변환
<br/><br/>

- time.asctime( time.localtime(time.time()))
: 보기 쉬운 형태로 현재 시간을 나타내 주는 함수
<br/><br/>

- time.ctime()
: time.asctime()은 인자를 받지만, ctime은 인자가 필요없이 현재 시간만을 나타내 주는 함수다.
<br/><br/>

# shutil

- shutil.copy( “파일1”, “파일2” )
: 파일1을 파일2로 복사 ( 동일 이름이 있을 경우 덮어씌우기 )
<br/><br/>

# random

- random.random()
: 0~1.0사이의 실수 중 랜덤 하게 리턴
<br/><br/>

- random.randint( 정수1, 정수2 )
: 정수1 ~ 정수2 사이의 정수 중 랜덤 하게 리턴
<br/><br/>

- random.choice( 리스트 )
: 해당 리스트 중 랜덤 하게 선택하여 리턴
<br/><br/>

- random.shuffle(리스트 )
: 해당 리스트를 랜덤 하게 섞어서 다시 리스트로 리턴
<br/><br/>

# webbrowser

- webbrowser.open(“웹 주소”)
: 웹 브라우저를 실행 시키고 해당 웹 주소로 이동<br/> ( 이미 웹 브라우저가 켜져 있다면 해당 브라우저에서 이동 )
<br/><br/>

- webbrowser.open_new(“웹 주소”)
: 웹 브라우저가 이미 실행 중이더라도 새로운 창으로 열리도록 이동
<br/><br/>

## 그외 
- platform.platform()
: 현재 사용중인 운영체제 정보 반환

#### ▶ 파일 전체경로 반환
- 윈도우 일경우
: os.path.join(os.getenv("HOMEDIRVE"),os.getenv("HOMEPATH"),"파일명"))
<br/><br/>

- 윈도우가 아닐 경우
: os.path.join(os.getenv("HOME"),파일명)


<br/>