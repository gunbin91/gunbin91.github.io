---
layout: post
title: "3. 오토스케일링( AutoScaling )"
tags: [ aws, autoscaling ]
date: 2020-01-13
categories: [ aws ]
---

<p align="center">
    수강신청이나 쇼핑몰의 타임세일등 특정시간이나 특정일에 사이트접속이 원활하지 못한것을 다들 경험해 보았을 것이다. AWS에서 제공하는 오토스케일링은 이를 좀 더 원활하게 해주는 서비스이다.
</p><br/>

<br/>

# ◆ AutoScaling(오토스케일링)
특정일 또는 특정시간대에 서버의 트래픽이 많아지고 그에따라 CPU사용량이 늘어날 때, <font color="orange">정책에 따라 시스템을 자동으로 늘리고 줄여주는 서비스</font>이다.

<br/>

## ▶ AWS AutoScaling 사용

#### 1. AMI(이미지)생성
오토 스케일링 작동 시 생성될 EC2인스턴스의 복사 이미지를 생성<br/>
이미지를 복사함으로서 빈깡통이 아닌, 서버(톰캣)이나 프로젝트파일(war)등을 모두 복사하여 불러올 수 있다.
- 1-1. AMI생성
: EC2 인스턴스 우클릭 -> 이미지 -> 이미지생성
- 1-2. 생성확인
: EC2 -> 이미지 -> AMI 이동( 생성된 이미지 상태값이 available이 되면 생성 완료 )
<img src="/assets/post_img/ami_create.PNG">

<br/>

#### 2. AutoScaling그룹생성
- 2-1. AutoScaling그룹생성
: EC2 -> AUTO SCALING -> Auto Scaling그룹 -> Auto Scaling그룹 생성
- 2-2. AMI선택
: 왼쪽 My AMIs(내 AMI)탭 선택 -> 생성한 이미지 선택(ami)
<img src="/assets/post_img/autoscaling_myami.PNG">
- 2-3. 인스턴스 유형
: 프리티어(선택사항)
- 2-4. 세부 정보 구성 -> 고급 세부정보
: <font color="orange">UserData(사용자 데이터)를 통해서 오토스케일링이 시작될 때 필요한 스크립트를 자동으로 실행</font>시킬 수 있다. 이곳에 작성한 스크립트나 파일은 <font color="orange">root권한</font>으로 실행된다.

> 오토스케일링 시 필요한 파일들은 모두 복사되어 오지만, <br/>톰캣은 중지상태로 옮겨지기 때문에 톰캣서버를 사용하는 프로젝트의 경우 톰캣을 실행시키는 쉘 스크립트가 필요하다. <a href="/etc/2020/01/10/etc_aws2_codedeploy.html">CodeDeploy포스팅</a>참조
<img src="/assets/post_img/autoscaling_userdata.PNG">

- 2-5. 기타옵션
: 나머지는 인스턴스 만들때와 동일 하게 적용하고, 키페어는 기존 키페어를 사용해도 된다.

<br/>

#### 3. 오토스케일링 예약 테스트
: 원래는 CloudWatch라는 모니터링 시스템을 통해 자동적으로 되어야 하지만, 트래픽의 증가를 예측할 수있는 시간대에서 예약을 걸어두고 사용할 수 있으며, 테스트용으로 사용할 수도 있다.

- 3-1. EC2-> AUTO SCALING-> 생성한 그룹 선택 -> 예약된 작업
- 3-2. 시작시간 UTC기준 시간으로 선택하여 생성하면 해당 시간에 인스턴스가 생성됨
- 3-3. 해당 인스턴스의 서버가 잘 실행되어 있는지 접속해보도록 하자!

<br/>
<hr/>