---
layout: post
title: "Eclipse 성능 향상(heap size 할당)"
tags: [ etc, eclipse heap size, 이클립스 성능 향상 ]
date: 2019-10-16
categories: [ etc ]
---

<p align="center">
    Eclipse의 메모리할당을 증가시켜 조금이나마 성능을 향상시킬 수 있는 방법에 대해 알아보자.
</p><br/>

## ◆ 이클립스 heap사이즈 늘리기
이클립스에서 시스템과부하나 메모리부족은 JVM의 메모리 사용영역에서 나타난다.
따라서 이클립스에서 해당 메모리 영역을 높여주면 보다 원활하게 작업할 수 있게된다.

> JVM의 실행영역은 Heap영역이 담당하고, 클래스 메타데이터 관리는 PermGen영역이 담당하게 된다.

<br/>

### ▶ Heap 사이즈 확인
Eclipse -> <font color="orange">Window -> Preferances -> Genaral</font> 에서 <font color="orange">Show heap status를 체크</font>해주면 이클립스 최하단에 사용중인 heap용량과 전체용량을 볼 수 있고, 그 옆에 스레기통 버튼을 클릭해 주게되면 가비지컬렉팅되어 메모리를 정리해준다.

<br/>

### ▶ Heap 사이즈 늘리기
&nbsp;<font color="orange">Eclipse 설치 폴더 -> eclipse.ini</font> 수정<br/>
해당 파일에서 'Xms256m'등의 사이즈가 표기되어 있는 항목이 두 개가 있는데, heap영역의 시작크기와 최대 크기를 타나낸다.<br/>
두개 다 <font color="orange">Xms1024m</font>정도로 해 두면 원활하게 이클립스를 사용할 수 있다.






<br/>
<hr/>