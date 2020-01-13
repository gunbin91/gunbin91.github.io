---
layout: post
title: "AWS1. Putty, WinSCP사용법<br/>(Window서버 putty접속하는 방법)"
tags: [ etc, aws, putty, winscp ]
date: 2020-01-10
categories: [ etc ]
---

<p align="center">
    AWS EC2 인스턴스에 원격 접속할 수 있는 Putty와 파일을 전송할 수 있는 WinSCP 사용법에 대해 알아보자. ( 여기서 EC2인스턴스의 생성법까지 다루진 않는다. )
</p><br/>

<br/>

# ◆ putty
&nbsp;<font color="orange">SSH접속(SSH의 포트는 default 22)이 가능한 터미널 에뮬레이터</font>로, Linux기반의 운영체제에서는 기본적으로 SSH서버가 설치되어 있지만, Window기반의 운영체제는 SSH접속이 기본적으로 설정되어 있지 않다.

> 단, <font color="orange">Window</font>에서는 Putty로 접근하는 방식을 주로 사용하지 않고,<font color="orange"> RDP(RemoteDesktopProtocol)원격 데스크탑 프로토콜(3389포트)을 사용</font>하여 접속한다. ( 물론 별도의 설정으로 Putty접속도 가능은 하다 )

<br/>

## ▶ Putty설치 및 사용법

#### 1. putty설치
<a href="https://www.chiark.greenend.org.uk/~sgtatham/putty/" target="_blank">https://www.chiark.greenend.org.uk/~sgtatham/putty/</a> 해당 사이트에서 다운받을 수 있다.

<br/>

#### 2. 프라이빗키 생성
Putty로 AWS linux인스턴스에 접근하기 위해서는 <font color="orange">private key가 필요하다. 인스턴스 생성시에 저장해 두었던 pem파일을 통해 생성</font>할 수 있다.<br/>
<font color="hotpink">
PuTTYgen실행 -> load -> AWS pem파일 선택 -> Save private key클릭 저장
</font>

<br/>

#### 3. putty 접속
putty실행 <br/>
-> SSH/Auth탭에 private key등록<br/>
-> Session탭 HostName에 DNS입력 ( Save버튼을 통해 저장하여 Load버튼으로 설정을 불러올 수 있다. )<br/>
-> AWS linux의 경우 login as: 라고 나오는데 ec2-user를 입력해주면 된다.<br/>
<br/>

아래와 같이 뜨면 성공
<img src="/assets/post_img/putty_connect.PNG" style="padding-left:0;">

<br/>

### ▶ Window인스턴스 Putty로 접근하는 방법
윈도우는 Putty를 통해 SSH로 접근하는 경우가 거의 없기 때문에, 기본적으로 SSH서버가 제공되지 않는다. 따라서 <font color="hotpink">Window서버를 Putty를 통해 접근하기 위해서는 SSH서버 설치가 필요</font>하다.

<br/>

#### 1. AWS윈도우서버 SSH서버 설치
window는 기본적으로 SSH서버가 설치되어 있지 않기 때문에 SSH서버를 설치 해야한다.<br/>
<a href="https://www.bitvise.com/download-area" target="_blank">https://www.bitvise.com/download-area/</a>에서 설치할 수 있다.

<br/>

#### 2. bitvise 설정
설치 후 <font color="hotpink">Settings -> Open easy settings -> Windows accounts탭에서 Allow login to any Windows account를 체크해야EC2 계정으로 접근이 가능</font>하다.

<br/>

# ◆ WinSCP?
파일질라와 같은 <font color="orange">SFTP파일전송 툴</font>이다. linux서버의 경우 특히 파일을 주고받기 더 까다롭기 때문에 파일전송에 유용하게 쓰일 수 있다.<br/>
( 마찬가지로 포트는 22를 사용한다 )

<br/>

#### 1. 설치
<a href="https://winscp.net/eng/download.php" target="_blank">https://winscp.net/eng/download.php</a>  에서 설치
<br/>
Putty를 먼저 설치하였다면, 설치 과정에서 putty에서 설정한 접속 정보를 불러올 수 있기 때문에 빠르게 접속할 수 있다.

<br/>

#### 2. 키 설정 및 접속
putty접속과 마찬가지로 호스트네임과 사용자이름을 적고 "고급"버튼을 클릭하여<br/>
SSH/인증 탭에서 private key를 등록하고 접속 할 수 있다.
<br/>

접속에 성공하였다면 아래와 같이 오른쪽에 접속된 서버의 파일리스트가 나오게된다.
<img src="/assets/post_img/winscp_connect.PNG" style="padding-left:0;">

<br/>
<hr/>