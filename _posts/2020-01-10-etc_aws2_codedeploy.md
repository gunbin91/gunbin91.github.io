---
layout: post
title: "AWS2. CodeDeploy<br/>( AWS S3를 이용한 배포 자동화 )"
tags: [ etc, aws, codedeploy, aws s3, appspec.yml ]
date: 2020-01-10
categories: [ etc ]
---

<p align="center">
    서버를 패치할 때 WinSCP를 이용하여 파일을 전송하여도 되지만, AWS의 CodeDeploy를 이용하면 서버재시작등의 쉘 스크립트 또한 함께 실행할 수 있다.
</p><br/>

<br/>

# ◆ AWS CodeDeploy
CodeDeploy는 Amazon EC2 인스턴스, 온프레미스 인스턴스, 서버리스 Lambda 함수 또는 Amazon ECS 서비스로 애플리케이션 배포를 자동화하는 배포 서비스입니다.<br>
라고 홈페이지에 설명이 나와있다. 간단히 말해 <font color="orange">배포 자동화 서비스</font>이다.

<br/>

## ▶ CodeDeploy 사용방법
초기 보안, 권한등의 설정으로 번거로울 수 있지만, 한번 설정해 두면 배포를 편하게 할 수 있다.

<br/>

#### 1. IAM ROLE(역할) 생성
EC2인스턴스에 S3와 CodeDeploy등의 권한을 부여하는 역할을 한다.

- 1-1. AWS IAM -> ROLE(역할) -> CREATE ROLE(역할만들기)
- 1-2. AWS 서비스 - EC2 선택
- 1-3. 아래 권한 정책 선택하여 다음단계로 이동<br/>
~~~
AmazonS3FullAccess
AWSCodeDeployFullAccess
AWSCodeDeployRole
CloudWatchLogsFullAccess
~~~
- 1-4. 역할이름 적고 만들기( ex) gunbin-ec2-deploy )
<img src="/assets/post_img/ec2_create_role.PNG">

<br/>

#### 2. EC2 생성 
- EC2 생성 시 Configure Instance단계에서 <font color="orange">IAM역할을 위 1번에서 만든 역할로 선택</font>한다.<br/>생성 후에도 연결할 수 있다.
- <font color="orange">태그추가</font> <br/> 배포 시 어떤 인스턴스인지 선택할 수 있도록 하기 위함 <br/> ex) 키: Name / 값: gunbin ( 이미 생성된 EC2에서도 변경 가능 )
<img src="/assets/post_img/ec2_tag.PNG">

<br/>

#### 3. CodeDeployAgent용 그룹 생성
S3와 CodeDeploy등의 접근권한을 가지는 <font color="orange">사용자의 키값을 만들기 위해 큰 범위로 그룹부터 생성</font>하여 해당 그룹으로 사용자를  만든다.

- 3-1. IAM -> 그룹 -> 새로운 그룹 생성
- 3-2. 정책연결 : 선택X (후에 JSON으로 작성예정)
- 3-3. 정책설정 : 생성된그룹선택 -> 권한 -> 인라인정책 -> "여기"클릭
- 3-4. 사용자 지정 정책 선택하여 정책검토탭으로 이동
- 3-5. 정책이름 설정 후 정책문서에 아래 내용 작성

{% highlight ruby %}
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "autoscaling:*",
                "codedeploy:*",
                "ec2:*",
                "lambda:*",
                "elasticloadbalancing:*",
                "s3:*",
                "cloudwatch:*",
                "logs:*",
                "sns:*"
            ],
            "Resource": "*"
        }
    ]
}
{% endhighlight %}

아래와 같이 생성된 권한을 확인할 수 있다.
<img src="/assets/post_img/deploy_agent_group.PNG">

<br/>

#### 4.  위 그룹에 사용자 추가
위 <font color="orange">그룹의 권한을 가진 사용자를 생성</font>하여 해당 사용자의 키값을 사용해 S3나 CodeDeploy권한등을 사용할 수 있다.

- 4-1. IAM -> 사용자-> 사용자추가
- 4-2. 사용자이름(ex) gunbin-deploy), 엑세스 유형: 프로그래밍 방식 엑세스 선택 다음
- 4-3. 그룹에 사용자 추가-> 3번에서 만든 그룹 선택
- 4-4. <font color="hotpink">.csv다운로드</font>( 퍼블릭, 프라이빗 키 필요 )<br/>중요한 파일이므로 잘 보관해 두도록하자.

아래와 같이 생성된 사용자의 권한이 위 3번에서 생성한 그룹에 속해야 한다.
<img src="/assets/post_img/deploy_agent_user.PNG">


<br/>

#### 5. EC2 인스턴스 환경설정
기본 설정 사항들은 모두 셋팅 되었으니 CodeDeploy를 위한 EC2 인스턴스의 환경을 셋팅해보자.

<br/>

##### 5-1. JAVA8 설치
{% highlight ruby %}
sudo yum update
sudo yum install -y java-1.8.0-openjdk-devel.x86_64
sudo /usr/sbin/alternatives --config java
sudo yum remove java-1.7.0-openjdk
{% endhighlight %}
설치확인 : java -version

<br/>

##### 5-2. cli설치 및 설정
- CLI설치
: {% highlight ruby %}sudo yum install -y aws-cli
cd /home/ec2-user/{% endhighlight %}

- CLI설정
: {% highlight ruby %}sudo aws configure
Access Key : csv파일의 AccessKey등록
Secret Access Key : csv파일의 SecretAccessKey
region name : ap-northeast-2
output format : json
{% endhighlight %}

<br/>

##### 5-3. Agent설치 ( 루비설치필요 )
{% highlight ruby %}
wget https://aws-codedeploy-ap-northeast-2.s3.amazonaws.com/latest/install
chmod +x ./install
sudo ./install auto
{% endhighlight %}
실행확인(PID) : sudo service codedeploy-agent status

<br/>

##### 5-4. Agent자동실행 쉘 스크립트 파일 생성
Agent를 인스턴스가 실행될 때 자동으로 시작될 수 있도록 스크립트를 등록

{% highlight ruby %}
sudo vim /etc/init.d/codedeploy-startup.sh // 파일생성

// 작성내용
#!/bin/bash 
echo 'Starting codedeploy-agent' 
sudo service codedeploy-agent restart
// esc-> :wq! 저장

// 실행권한 추가
sudo chmod +x /etc/init.d/codedeploy-startup.sh
{% endhighlight %}

<img src="/assets/post_img/ec2_instance_environment.PNG">

<br/>

#### 6. 배포파일만들기
war파일을 사용하는 Spring파일을 기준으로 배포하는 방법에 대해 알아보자.

- 6-1. 배포할 war파일 추출
- 6-2. <font color="orange">appspec.yml</font>파일을 만들어 아래 내용을 입력하고 <font color="orange">war파일과 같이 .zip파일로 압축</font>
{% highlight ruby %}
version: 0.0
os: linux
files:
  - source:  /
    destination: /home/ec2-user/build/
{% endhighlight %}
- source
: 해당 프로젝트를 어디서부터 추출할 것인지에 대한 경로
- destination
: 배포할 EC2경로( 즉 EC2에 해당 경로가 있어야 함 )
- 6-3. <font color="orange">압축한 배포파일을 AWS S3버킷으로 업로드</font> 시켜둔다. ( AWS S3를 미리 만들어두자 )

<br/>

#### 7. CodeDeploy
본격적으로 배포할 수 있는 단계이다. 해당 단계가 끝나면 EC2인스턴스로 배포파일이 업로드된다.

- 7-1. CodeDeploy 역할 생성
: IAM-> 역할-> 역할만들기-> AWS서비스/CodeDeploy선택 -> AWSCodeDeployRole선택
<img src="/assets/post_img/deploy_role.PNG">
- 7-2. 애플리케이션 생성
: CodeDeploy-> 애플리케이션 생성-> 컴퓨팅 플랫폼: EC2/온프레미스-> 생성
- 7-3. 배포그룹 생성
: CodeDeploy-> 애플리케이션-> 생성한 애플리케이션 선택-> 배포그룹-> 배포그룹생성 <br/>
~~~
Service role(서비스역할): 7-1에서 생성한 역할 선택
Deployment type(배포유형): 현재위치배포
Environment configuration(환경구성): EC2인스턴스
Tag group(태그): 배포할 EC2인스턴스의 태그 이름/값
~~~
<img src="/assets/post_img/create_deploy_group.PNG">
- 7-4. 배포
: CodeDeployt-> 애플리케이션-> 생성한 배포그룹 선택-> 배포생성<br/>
개정 위치: ex) s3://S3버킷네임/배포파일.zip

<br/>

> 이후부터의 <font color="hotpink">배포 과정은 6->7-4 두 단계의 과정만 반복</font>하여 진행된다.

<br/>

#### * 참고
- 리눅스 톰캣설치
: https://jeongyd.tistory.com/51

- 파일 접근권한 변경
: chmod 777 -R 디렉터리<br/>
( -R 옵션은 해당 디렉터리 내부까지 모두 포함하여 권한 변경 하라는 뜻이다. )

<br/>

## appspec.yml 좀 더 활용해보기
war파일을 배포한다고 해서 프로젝트에 바로 적용되는 것이 아닐 것이다.<br/> 배포 후 서버를 재시작 하는 등의 스크립트 작업이 필요한데, 이를 AWS CodeDeploy는 배포할때의 과정을 나누어 중간중간 쉘 스크립트를 실행할 수 있도록 제공한다.

- CodeDeploy LifeCycle
: <img src="/assets/post_img/lifecycle-event-order-ecs.png" style="padding-left:0;">

<br/>

#### appspec.yml 작성예시
{% highlight ruby %}
version: 0.0
os: linux
files:
  - source: /
    destination: /usr/local/apache-tomcat-9.0.30/webapps/
    
permissions:
  - object: /usr/local/apache-tomcat-9.0.30/webapps/
    pattern: "*"
    owner: root
    mode: 777
    type:
      - file
hooks:
  AfterInstall:
    - location: scripts/after_deploy.sh
      timeout: 300
      runas: root
{% endhighlight %}
- permissions : 배포파일 권한 바꾸기
- hooks: 배포 쉘 스크립트 실행 타이밍과 스크립트 파일경로 지정<br/>
( <font color="orange">쉘 스크립트는 배포할때 같이 있어야 함</font>. 즉 EC2가 아닌 배포되는 파일 zip내부 )

<br/>

#### * sh파일 작성법
- 쉘 스크립트 
: 인터프리트 방식(기계어변환(컴파일)없이 바로 실행할 수 있는)으로 동작하는 컴파일 되지 않은 프로그램
- sh파일 
: 쉘 스크립트를 작성하여 실행할 수 있느 파일
- sh파일 작성 방법( ex) 배포 후 톰캣 재실행 )
: {% highlight ruby %}
#!/bin/bash  
cd /usr/local/apache-tomcat-9.0.30/bin/
shutdown.sh
startup.sh
{% endhighlight %}
- <font color="orange">첫 줄은 해당 쉘 스크립트가 어떤 스크립트인지 알려주는 역할</font>을 한다. 위 스크립트의 종류는 bash쉘임을 알려주는 역할을 하고, 해당 인식코드가 <font color="orange">필수</font>적으로 있어야 스크립트를 인식할 수 있다.
- 주의 ) <font color="orange">윈도우에서 메모장으로 작성한 sh파일은 리눅스에서 인식될 수 없다.</font>

<br/>

- 배포로그  실시간 확인
: {% highlight ruby %}tail -f /opt/codedeploy-agent/deployment-root/deployment-logs/codedeploy-agent-deployments.log{% endhighlight %}

<br/>
<hr/>